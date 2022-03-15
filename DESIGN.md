I used a similar format to CS50 Finance for my project in which I used an initial layout html page with other html pages extending the initial page. First, in addition using an error page similar to that of Finance, I implemented a guide page for less egregious errors and provided a redirect button to make navigation easier for the user. These guide pages were used for mistakes with logging in and registering where the user may have made a careless error. 

Logging in and registering was implemented very similarly to Finance and utilized a similar users database which also stored the user’s bio and musical genres of interest.

Upon registration, I redirected the user to an information page. The information page was used to gather the user’s bio using a text area and genres of interest using checkboxes. The genres were concatenated into a singular string from the checkbox inputs for use in the user profile. Moreover, every time this page was revisited, the user’s genres of interest and bio were pre-filled on the page through SQL queries. Note that both the bio and genres are optional and may be left empty.

Next, for searching, I implemented a SQL query using LIKE to find users matching the search. The results are displayed as cards each of which contains a button redirecting to the corresponding user’s profile through a post submission to profile encoding the user.

For user profiles, I implemented both the current user and other user profiles using the same html file so as to avoid repetition. Making use of if statements in jinja, I rendered the “Edit profile” button for the current user’s profile to redirect to the information page and rendered the “Follow/Unfollow” button for all other users beside the current user.  I used only get requests for profiles as I was only displaying information; however I did use a form to submit the specified user for profile rendering. For the value of this submission I made sure to use a user’s username and not their id as to protect the their information. If no username was submitted, the profile defaulted to that of the current user.

For following, I created a new database with follower and followed categories referencing id from users. I queried	 the database to determine whether the current user should be displayed the follow or unfollow button  when viewing another user’s profile and changed the database accordingly when the follow or unfollow button was clicked.

For messages, I created a similar table with sender and recipient categories referencing id from users as well as a message and datetime column. For my initial messages page I created a button opening a dialogue form allowing the current user to select who to send a new message to from all the users they followed. I also buttons directing to conversations with users the user had previously received or sent a message to. I queried my messages table and used a set to ensure this list of users was unique. Upon opening the messages page, I listed all messages in chronological order between the current user and specified user and indicated (through CSS styling) who the sender and recipient was. 

For posting, I made use of file I/O provided by Flask through the request.file.get and send_from_directory functions. I implemented posting through a dialogue form with a caption texture and file upload on the current user profile and saved the uploaded files to a /audio folder inside the project directory, ensuring that the file type was only .mp3 or .wav. To display these files so that they could be played, I used the <audio> html tag and send_from_directory to create a url from the /audio folder path with the specified file name. I displayed these posts on user profiles and made them only visible to followers. I also displayed these posts on the homepage, which displayed all posts from users followed by the current user in chronological order. I used another database for posts referencing users for the associated poster and also included the filename for url generation and content type for the html tag.

In general my styling made use of the Bootswatch Lux stylesheet with an additional stylesheet of my own to accommodate any additional stylistic specifications.