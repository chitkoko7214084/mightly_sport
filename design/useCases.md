# Mighty Sports — MVP Use Cases

## Use Case 1: Register Team
**Actors**: Coach, System  
**Preconditions**: Coach has access to the registration form.  
**Steps**:  
1. Coach opens **Team Register** form.  
2. Coach fills in required fields (Coach Name, Email, Phone, Team Name, League/Division, etc.).  
3. Coach agrees to rules and signs.  
4. System validates inputs.  
5. System generates unique **Team Code**.  
6. System stores team data in Firestore.  
7. System displays success message with Team Code.  
**Postconditions**: Team is registered and available for players to join.  

---

## Use Case 2: Register Player
**Actors**: Player, System  
**Preconditions**: Player has valid Team Code and required documents (headshot, ID).  
**Steps**:  
1. Player opens **Player Register** form.  
2. Player fills in fields (Name, DOB, Email, Phone, Team selection, etc.).  
3. Player uploads headshot and photo ID.  
4. Player checks consent and signs.  
5. System stores player data (status = Pending).  
6. System sends confirmation email: "Status: Pending."  
**Postconditions**: Player registration is stored as Pending until Admin verifies.  

---

## Use Case 3: Verify Player (Admin)
**Actors**: Admin, System  
**Preconditions**: Player has submitted registration.  
**Steps**:  
1. Admin logs into **Admin Panel**.  
2. Admin reviews submitted documents and details.  
3. Admin selects **Verify** or **Needs Fix**.  
4. System updates player status.  
5. System triggers Cloud Function to send micro-email.  
   - Verified → "You’re Verified for {TeamName}"  
   - Needs Fix → "Can’t verify — reason. Fix here: {link}"  
**Postconditions**: Player status updated, directory reflects verified players.  

---

## Use Case 4: Browse Directory
**Actors**: Public User, System  
**Preconditions**: At least one verified player exists.  
**Steps**:  
1. User opens **Directory** page.  
2. User filters by league, team, or player name.  
3. System displays **cards** with Headshot, Name, Team, Coach, League, and Verified badge.  
**Postconditions**: Directory is browsed without exposing private information.  

---

## Use Case 5: View Rules
**Actors**: User (Coach, Player, Public), System  
**Steps**:  
1. User navigates to **Rules** page.  
2. System displays eligibility, ID, roster, conduct, fees, seeding, and privacy policies.  
**Postconditions**: User has access to rules and requirements.  

---

## Use Case 6: Lock Roster (System Automation)
**Actors**: System  
**Trigger**: Reaching Week 3 or roster lock date.  
**Steps**:  
1. Cloud Function checks date.  
2. System prevents new players from registering to teams.  
3. Admin can still override manually.  
**Postconditions**: Rosters locked automatically.  

---

## Use Case 7: Export Verified Roster
**Actors**: Admin, System  
**Preconditions**: At least one team has verified players.  
**Steps**:  
1. Admin requests export.  
2. System queries Firestore for verified players.  
3. System generates CSV/PDF roster.  
4. System provides download or sends via email.  
**Postconditions**: Admin has offline copy of rosters.  
