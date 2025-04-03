# Week Ten - SPRINT WEEK

## Monday 24/03/2025

### During Session
- The first day of sprint me and Jasmine continued on our work from last week. We had originally planned to only spend Monday solving issues, and the rest of the week debugging, but we ran into a lot of issues on Monday. We spent this day figuring out how to configure a login system using Authentication and Authorization in Blazor. We had worked on this the previous week as well, and got quite far with it, but we still ran into the issue where users weren't being passed through authentication. We were able to authorize page views accordingly, but no user at all could access these pages. Most of the day was spent looking into this as it was crucial that (e.g.,) a candidate can not look at a staff dashboard.
- Eventually password hashing worked and could compare the key of the hashed password in the database to the users inputted password. But the page view authorization still didn't work for any logged in user.
- We figured out that the issue likely lied in how the Cookies were handled in the program.cs in the builder services, which stores the authorized state of the user. We tried adding some builder services for staff and candidate, as well as some functions like app.UseAuthentication(); but it still wouldn't run properly.
- We referenced this Microsoft documentation to try and understand why it wasn't working and how to go about building it: https://learn.microsoft.com/en-us/aspnet/core/blazor/security/?view=aspnetcore-9.0&tabs=visual-studio
- This video was also followed: https://www.youtube.com/watch?v=GKvEuA80FAE&ab_channel=CodingDroplets
- This was the whiteboard used for planning out our day for the first day of Sprint Week where our tasks were divided and documented the tracking: (proof_and_screenshots\sprintweekboard.png)

### To Do
Figure out why the authorization isn't working
Do some research on cookies and find the best way to handle them for authorization

### Issues
Authorization not allowing us to see any pages. We were working off our own branch so this didn't halt the progress of our other members, but we were halted on our end with not being able to access any login-required pages.

## Tuesday 25/03/2025

### During Session
- To start this session off, we decided to take a break from authorization as we weren't getting far with it and it caused us to just be confused. So, we instead started with an Admin adding a new Staff member to the database. We decided an Admin should only be able to add a Staff member because it is highly unlikely that a Staff member should be able to add one of their peers, for example. This was quite easy as it was just the same as adding a Candidate, except changing the values and adding in StaffId (their staff number) to the input values. We created the page for this and added in what should be where it authorizes the Admin to only view and edit on this page.
- We then did page logout, because I decided to email Arian about the page authorization and see if he could help us at all. While I waited for his email reply (proof_and_screenshots\arianconsult.png). To do this, we had to find a way to clear the users cookies after they logged out. We have it set up so after 30 minutes, they are timed out, and cookies are removed from the user so they will have to login again. This was general safety practice (e.g.,) if someone were to leave their laptop open in public. We did so by adding a MaxAge(30) to the cookie builder, which clears the cookies after the maximum age of 30 minutes.
- We then took another try at authorization, but got nowhere with it again. We kept getting this error: "No authenticationScheme was specified, and there was no DefaultChallengeScheme found."
    - We looked on a few Stackoverflow links to try and fix this bug, as we figured it probably was due to our double instantiation of cookies for different types of users. So originally, we had it that Staff and Candidate were on two instances of Builder Services for cookies, but this led to that error. The links we looked at were:
    https://stackoverflow.com/questions/75683753/no-authenticationscheme-was-specified-and-there-was-no-defaultchallengescheme 
    https://learn.microsoft.com/en-us/answers/questions/1164459/exception-scheme-already-exists-when-trying-to-imp
- Arian then replied but we were quite busy doing the logout and adding staff as we didn't want to stop development due to this, so me and him planned to call tomorrow and see if he could advise on how to go about our issue. He said he knew the problem we were having, so I told Jasmine I would take on all the login, authorization, and authentication from here on out as I was the one having communication with Arian.


### To Do
Completed all for this session

### Issues
Authorization still not working
Cookies only clear after 30 minutes, but we wanted them to fully delete on log out. After some research we found out this could be quite difficult to do as you have to overwrite the current cookie with a negative time value (e.g., MaxAge(-1D)) to wipe it. We left it as the 30 minute clear and logout for now, deciding if we have more time to implement that after I consult with Arian.

## Wednesday 26/03/2025

### During Session
- Me and Arian joined a Google Meeting at 10am and I explained the situation with the authentication and authorization and gave a brief overview of why I thought it was happening. We started off by fixing the previous issue with the cookies I mentioned. This was an issue because of the cookie builder being ran twice for a Candidate and Staff. So, first off, we changed it so the builder service set to a DEFAULT which would apply to all users. 
- After this, Arian showed me how to use the Identity service which was actually built into Blazor. He explained that the issue we were having was due to a few things:
    - We were hashing and salting the passwords ourselves with a function me and Jasmine made for Staff and Candidate. With the built in Blazor/Microsoft/Asp.Net Auth, if you build the tables properly within the database and install the correct package, you don't need to do this. This is partly why once logged in, even though the passwords were getting checked, the view authorisation still wasn't working.
    - We hadn't installed the correct package for Microsoft.AspNet.Identity in our library.
    - We hadn't done a database migration for the AspNet tables to be made in our database, therefore it wasn't using any of the verification from there even though we had written the code where it required that. But we didn't know as when me and Jasmine did the password auth it wasn't mentioned in the tutorials we were following.
- After adding Identity services, I rebuilt the structure of the builder services for cookies as well as the app.UseAuthentication and functions such as that. Arian said that the issue might occur due to the format in which they are ran in the program.cs so those were changed and fixed to be in the correct format.
- Next, we went into the actual files where the candidate registers and login. Liana swapped out with me for an hour as she knew more about migrations than I did, and I felt more comfortable if she did that bit due to not wanting to lose data if I misdid a migration. So, Arian told us to run new migrations, and the database updated with the correct AspNet tables that allowed for the prebuilt hash function, and things for a UserManager in order for us to manage the users that register and how their login is handled. 
- I followed this on each page to add the Authorize View, which was sent by Arian to explain it better to me: https://stackoverflow.com/questions/75946661/blazor-server-authorization-to-access-page
- Then I started redoing the authentication code for register and login pages so that it worked with the new database tables and the LoginModel created by Liana. I used the UserManager function to get respective roles (candidate/staff). Then, Arian showed about the claims. Me and Jasmine had previously had Claims in the code, but it wasn't fetching for the specific user. I created a new list of claims specific to the candidate login input, which then ran through the Identity and would only log the user in if true. (proof_and_screenshots\claims.png)
- I created the register model code very similar, except it didn't use claims since it was adding a Candidate. For this, I changed the AddCandidate() function to register a new user using the NextUser model which inherits IdentityUser. In the NextUser model I added FirstName and LastName so when a candidate registers they have to enter that, and the IdentityUser defaults to needing things such as Email, UserName, etc. (proof_and_screenshots\register.png)
- After sorting out everything with Arian and him explaining the main bits that were causing the issue, he left me to finish the rest by myself as I had a pretty solid understanding of what was happening and how to fix it. I went through each of the LoginPages (CandidateLogin, Logout, Register, StaffLogin) and fixed the html so the new values were binded to those required of the IdentityUser. 
- Once I fixed the code on all the LoginPages, I wrote and queryed in some results for the encouraging messages. Liana created the table and me and her spoke about the frequency of the messages. We ran a few test examples and did some math for this, which she then wrote in the code. (proof_and_screenshots\encouragingmath.png)

### To Do
Fix up all CRUD pages to match new Authentication and make sure the Authorisation of viewing for certain users works on every page.
Create a Cookie agreement so the user can only proceed with the quiz if they accept our terms.
Clean up/delete default Blazor pages

### Issues
No conflicts this session

## Thursday 27/03/2025

### During Session
- After yesterday, me and Liana decided to work on the CRUD pages together for the rest of the sprint. We both made a list of all CRUD pages that needed to be changed to have authorisation (proof_and_screenshots\thursdaytasks.png). In the blue writing is what had been completed thus far, and the bottom left where it says Staff, Candidate, Admin, is what needed to be done. We split this up and worked together just to get it completed. 
- I encountered a bug when trying to run the pages after adding Authorisation to the html where it encapsulated an EditForm function, (proof_and_screenshots\thursdaybug.png). After some research, Stackoverflow and Reddit suggested this fix: https://stackoverflow.com/questions/77385602/component-editform-uses-the-same-parameter-name-context-as-enclosing-child
    - To my understanding, it was due to having multiple context's for the AuthorizeView, as I didn't set a certain name for the context. Though, at first, I thought it was an issue with the EditForm context. As you can see in the screenshot attached, I tried adding a EditContext variable, but was still encountering the error. I emailed Arian as the error still wasn't resolved, but by the time he had replied I had figured it out that it was the context for the AuthorizeView I needed. I resolved this by setting the Context to a "authContext" variable and then went onto every page that had an EditForm inside the AuthorizeView and changed their context to that as well (proof_and_screenshots\error-resolved.png).
- I completed (alongside Liana) all the Candidate, Staff, and Admin CRUD. This included changing links, setting the roles for the view, and some other pages such as the Index, Results, and Details page for the respective user. After this, I started on adding Cookie Authorisation to the landing page.
- For the cookie authorisation, it was very straight forwards. I created a popup in the Home page, where the user can ONLY proceed to the landing page/quiz if they accept the terms. This is due to following the briefs requirements, where user data will be taken from their results in order for staff to analyse which roles and departments are recommended more to users. The way I set up the cookies the previous day actually sets the cookie after the user starts the quiz, so I didn't need to add anything that creates the cookie after the user clicks Agree on the popup. For the text provided in the Cookie Banner, I researched on GDPR and on the UK Government website to see what information was mandatory to show to a user when taking their cookies. I followed the required information, and also added a link which redirects the user to the NEXT Careers PDF on their cookie usage and agreement if they want further information. (proof_and_screenshots\cookie.png) Liana found the cookie icon on Google icons which I added to the css, and then she helped me with a CSS issue I was having. I wrote it so that on initial load, the cookie banner is shown and the background opacity is lowered. Then, when a user accepts, the banner should be hidden and background at full opacity. It was throwing an issue where it would stay shown after click, so Liana helped me out with this and we decided the easiest way to go about it was writing two lines of code for it instead of doing an inline one line. This worked well, except added an extra class to the CSS but we didn't mind as it worked well. Liana made a cookieService which we added to the Cookie Popup code, so that if the user consented, the state was set to true and it wouldn't reappear every time they reloaded the site. 


### To Do
Fully clean up Dashboard Pages (with the new CRUD)
Go through and decide which pages are needed
Merge all to dev

### Issues
We had some issues with the amount of work being completed on time. This was particularly an issue due to me and Liana having spent the entire day practically reworking all the CRUD pages, and despite our work, there were still tasks not completed on time by another teammate that pushed back the schedule. The charts that connected the result data to the dashboard were started on Monday and needed to be completed by this morning so that we wouldn't fall further behind schedule. However, this teammate still didn't complete it and refused to ask for help or communicate their struggles with the rest of the team.

## Friday 28/03/2025

### During Session
- The session started off by visualising which pages we needed, and which we could delete, alongside which were fully functioning (for CRUD). We ended up deciding on the pages written on the board as which a user would need (proof_and_screenshots\fridaytask.png). 
- I started working on the Candidate functions in the Delete and Edit page. I figured this would be the best way to go about it, as the pages the day before had been fixed with authorisation, but some code still needed to be changed to reflect the new models added. I told Liana it would probably be best if I did the Candidate Edit and Delete, and then she could replicate that code but for Staff/Admin. This was mainly due to me being a bit more familiar with the authentication/authorization as I had done the majority of that with Arian and had a good understanding of it.
- I encountered an error when trying to delete a Candidate (proof_and_screenshots\deletecandidate.png). After looking through some sources, such as https://stackoverflow.com/questions/77812187/asp-net-identity-library-delete-user-does-not-delete-their-claims, and https://learn.microsoft.com/en-us/dotnet/api/system.security.claims.claimsidentity.removeclaim?view=net-8.0, I figured out that my issue was occuring because I wasn't calling the LoginModel correctly. To fix this, I did a getter and setter for the LoginModel, like I had done before, but this time set it to a new();, as well as removed the Claim properly before calling the DeleteAsync, so that the user is completely wiped from our records. This was done for privacy issues as we shouldn't hold user data if a user chooses to delete their account and no longer wishes for us to hold their personal data.
- I then did the Edit page. This required making a new model as we couldn't fetch the information to update it with the Login Model. Liana suggested making a Edit Model, and then I put in the same information that is used in the Login Model, but this time added CurrentPassword. This way, it updates the password and hashes it. The issue we were having and why we chose to create and Edit Model was because all the other information, such as email, was getting updated, but since the password was hashed it wasn't updating it. So it would just revert to the initial set of the password entered. By creating this model, it also helped for overwriting and setting the new information, so that login still worked even with updated information.
- After this, all functions we had needed to fix was completed. I helped Liana out a bit by explaining how it worked for Candidate so she could implement it for the staff pages like said before. The only issue we encountered with this was for deleting a staff member as it ran a check through the Id (their staff number) as well. We resolved this by setting it for admin view only, and then eliminating the need for their staff number to be checked against and just used their user Id instead. 
- Then, me and Liana did lighthouse testing, as well as researched what needed to be put in our testing plan. We did a rough draft of things that needed to be spoken about in the testing plan, as we were waiting on another teammate to still finish up the charts before we could start merging everything to dev. We ran a lighthouse report on all pages, documented down what needed to be improved, and put it in the document so the members who were meant to do the testing could use what we had already. (proof_and_screenshots\lighthouse.png)


### To Do
Merge to dev, test it
Do the presentation
Record the software
Present on Monday to client

### Issues
The main issue we encountered again was the issue with the teammate not completing their work on time. We had originally planned to get everything done at 2pm, then to push to dev, solve conflicts, and do the presentation. Due to another teammate still working on the charts from Monday, we couldn't do this and had to wait on his work to be completed. I said I would do the presentation over the weekend, and I would solve the merge conflicts as a lot of the code being pushed had been done in mine and Lianas Login-system branch. Therefore I knew what needed to be kept, and I communicated this to the member who hadn't completed the work on time that they would just have to resolve their own merge conflicts from the charts. This is expanded on in my reflection, due to some stuff happening over the weekend that isnt included in the sprint.

