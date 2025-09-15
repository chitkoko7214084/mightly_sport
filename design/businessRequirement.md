# Business Requirements – Mighty Sports MVP  

## 1. Purpose  
Mighty Sports needs a lightweight MVP system to manage sports league registrations, player verification, and a public player directory. The system should simplify the workflow for coaches, players, and admins while ensuring data privacy and compliance.  

---

## 2. Scope  
The MVP will provide:  
- **Web-based navigation** with four tabs: **Team Register, Player Register, Directory, Rules**.  
- **Team Registration** for coaches with auto-generated Team Codes.  
- **Player Registration** tied to teams with pending/verified status.  
- **Admin verification flow** for ID and roster management.  
- **Public directory** with filters, displaying verified player profiles only.  
- **Micro-email notifications** for coaches and players.  
- **Roster management rules** (max 15, lock by Week 3).  

---

## 3. Functional Requirements  

### 3.1 Navigation  
- Simple nav bar with: **Team Register, Player Register, Directory, Rules**.  

### 3.2 Team Registration (Coach)  
- Input fields: Coach Name, Email, Phone, Team Name, League/Division (select), City (optional), Jersey Primary/Secondary (optional), Agree to Rules (checkbox), Signature, Date.  
- System generates a **unique Team Code** upon success.  
- Success message: *“Team registered. Your Team Code: {TEAMCODE}. Share with players.”*  
- Confirmation email sent to coach.  

### 3.3 Player Registration  
- Input fields: Name, DOB, Email, Phone, Team (select/search), Jersey # (optional), Position (optional), Headshot upload, Photo ID upload, Consent checkbox, Signature, Date.  
- System marks player as **Pending** until admin verifies.  
- Success message: *“Thanks! Status: Pending. We’ll verify your ID & team.”*  
- File upload rules: Headshot clear, no hats; ID must show name & DOB; blurry = rejected.  

### 3.4 Directory (Public)  
- Filters: **League, Team, Player Name**.  
- Directory card shows: Headshot, Name, Team, Coach, League, Verified badge.  
- Excludes: DOB, phone, email, ID.  
- Only verified players are displayed.  

### 3.5 Rules Page  
- Static page listing rules (Eligibility, ID, Rosters, Check-in, Conduct, Fees, Seeding, Privacy).  
- Accessible publicly.  

### 3.6 Admin Flow  
- Coaches register → Team Code generated.  
- Players register → Marked Pending.  
- Admin verifies ID & team → Player marked Verified or Needs Fix.  
- Automatic roster lock on Week 3.  
- Directory updated only with Verified players.  

### 3.7 Micro-Emails  
- **Coach:** “Team {TeamName} registered. Team Code: {TEAMCODE}. Rules: {link}.”  
- **Player Pending:** “We got your registration for {TeamName}. Status: Pending.”  
- **Verified:** “You’re Verified for {TeamName}. Bring photo ID.”  
- **Needs Fix:** “Can’t verify—{reason}. Fix here: {link}.”  

### 3.8 Data Requirements  
- **Team:** id, teamName, league, coachName, coachEmail, coachPhone, jerseyColors, createdAt.  
- **Player:** id, name, dob, email, phone, teamId, headshotUrl, idHash (private), status (Pending/Verified), createdAt.  

---

## 4. Non-Functional Requirements  
- **Privacy:** No selling/sharing data; store only ID hash, not full ID image.  
- **Security:** Firebase Authentication & Firestore security rules.  
- **Scalability:** Support multiple leagues/divisions.  
- **Accessibility:** Mobile-responsive design.  
- **Usability:** Clear success/error messages.  

---

## 5. Launch Checklist  
- Google Forms (Team, Player) integrated with Sheets.  
- Simple Vue site (3 tabs + Rules) linked to Firebase/Sheets.  
- Admin View (Sheets/AppSheet or custom panel) to verify players.  
- Print/export roster function for Verified players per team.  
