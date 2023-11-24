# Trello REST API testing with Postman
## :mag_right: About project
## :clipboard: Test scope based on [Trello API Documentation](https://developer.atlassian.com/cloud/trello/rest/api-group-actions/#api-group-actions)
## :electric_plug: How to get started?
#### :pushpin: List of steps needed to run collection and tests:
:one: [Postman installation](#one) 

:two: [Creating a Trello acount](#two)

:three: [Trello authentication](#three)

:four: [Importing a file into Postman](#four)

:five: [Creating environment variables in Postman](#five)

:six: [Run collection and testing](#six)

--------
#### <a name="one">:computer: Postman installation</a>
1. Go to the Postman website and click the orange button with name of your operating system.
2. Download the installation file, then run the installer and follow the instructions that appear.
3. Postman is ready to use.

#### <a name="two">:e-mail: Creating a Trello account</a>
1. Go to the Trello website and click the blue button with text "Get Trello for free".
2. Create a Trello account by following the instructions that appear.
3. Your Trello account is ready to use.

#### <a name="three">:key: Trello authentication</a>
1. Log in to your Trello account.
2. Go to the Trello developer API key generation page.
3. Click on the "Go to the Power-Up Admin Portal", then click "Create New Key" button and enter the required details.
4. Your API key will be displayed on the page. Copy and save it for later use in Postman.
5. Next, click on the Token link that appears under the key you just generated.
6. Allow application to access your Trello account.
7. Your token will be displayed on the page. Copy and save it for later use in Postman.

#### <a name="four">:open_file_folder: Importing a file into Postman</a>
1. Go to my Postman collection file.
2. Click on the three dots icon in the top right corner and click "Download".
3. Run Postman and click on "Import" button in the top left corner.
4. Drag and drop the downloaded file from the Download folder into the "Import" window.
5. The collection will appear in Postman, ready for use.

#### <a name="five">:earth_africa: Creating environment variables in Postman</a>
1. Click on the "Environment" dropdown in the top left corner in Postman.
2. Click on the "New" button to create a new environment and choose "Environment" icon.
3. Give your environment a name.
4. Create a "key", "token" and "baseURL" variable. You should enter the value "https://api.trello.com/1/" into the "baseURL" variable and the value of your key and token in the "key" and "token" variable. For collections from this repository, the API key variable is named {{key}}, the token variable is named {{token}} and the URL variable is named {{baseURL}}.
5. Click "Save" button to save the environment.
6. Click on the "Environment" dropdown in the top left corner and select the environment you just created.

#### <a name="six">:arrow_forward: Run collection and testing</a>
1. Click on the "Collections" icon in Postman.
2. From the list of collections, select the one named "Trello - REST API" and click on the icon with three dots that appears when you hover over the collection name.
3. Select "Run collection" from the list.
4. Click one the orange button "Run Trello - REST API".

-------
### :point_down: If the view in your Postman looks like the one on the screenshot below, then you have successfully completed all the steps and run my collection. CONGRATULATIONS! :clap:
