# Code-Summary-C-Sharp Front End
## Introduction

After the first two week of the C# Live project, it was time for my two week sprint of front end work. I Enjoyed the 
C# project enough to choose to to stick with it through my front end sprint as well. I knew the biggest challenges for
me through the front end string was going to be staying intrinsically motivated because it doesn't interest me nearly as 
much as the logic driven back end work does. I was happy to find success in the stories I accomplished regardless.

### Week 1

##### The Problem #1

My first task for my front end sprint was to make the landing page more directive to new users. I needed to make more
straight forward links for users to register, log in and have a link to the clients official home site. I also had to 
welcome the user and inform them that they had reached the employee portal. On it's surface this was simple. Because I
am still in the habit of over thinking some tasks I am often wondering if the solution is as straight forward as I think
it is. More often then not, the task is simple, I already know the solution and all there is to do is go with my gut 
instinct and implement it. 

##### The Solution #1

Since the code for everything that I needed to make a link to already existed, I knew I had to find a way to draw 
attention to them in an aesthetic fashion. My first attempt let me to displaying the links in a vertical column that 
left way too much white space on the side of the page. In addition to that, The links were basically plain text with 
nothing drawing the eyes to them. After this I looked into a different approach. I found placing the links horizontally
was much more aesthetically pleasing and took care of the write space. In addition to that, I also placed a border 
around each of the links to draw attention to them. Below is the code I wrote to achieve all of that. Even though this 
was not a super difficult story, it was the best one to start my sprint off with and built my confidence nicely.

    }
    <h1>Welcome To Erectors Inc.</h1>
    <div class="container">
        <div class="row">
            <h4>You have reached our company portal for new and current employees.</h4>
        </div>
        <div class="row">
            <div class="panel-group top-buffer col-lg-4 ">
                <div class="panel panel-default ">
                    <div class="panel-heading">
                        <div>
                            <h4>Are you looking for our main website?</h4>
                            <a href="https://www.erectorsinc.com">Take a look</a>
                        </div>
                    </div>
                </div>
            </div>
            <div class="panel-group top-buffer col-lg-4 ">
                <div class="panel panel-default ">
                    <div class="panel-heading">
                        <div>
                            <h4>Already a registered employee?</h4>
                            <a href="/Account/Login">Log in here</a>
                        </div>
                    </div>
                </div>
            </div>
            <div class="panel-group top-buffer col-lg-4 ">
                <div class="panel panel-default ">
                    <div class="panel-heading">
                        <div>
                            <h4>New employee waiting to register?</h4>
                            <a href="/Account/CheckCode">Register here</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>    

##### The Problem #2

My next front end task was to develop a dashboard specifically for mobile users. More specifically, my task was to 
create a page with four buttons linking to the chat, manage account, jobs and manage accounts page. This was an 
interesting one because I was required to detect if the user was on a mobile device or not. 

##### The Solution #2

Detecting a mobile device was my first step to this problem. With the story I was given a link to a tutorial with code
to do this. I didn't know at the time but the code was compatible with asp.net but not MVC. This was a productive hurdle
because the code I eventually wound up using was in the tutorial, it was just surrounded by a lot of filler I had to dig
through. Learning the answer might be right in front of you and just has to be examined and worked into the environment
you are currently using was an imported lesson. After some research, I was able to find a simple line of code to detect
a mobile user in MVC. It's posted below.
       
       if (Request.Browser.IsMobileDevice)
            {
                return RedirectToAction("MobileDashboard");
            }

After that code was found, I had to research how to make it seem like I was on a mobile device on my browser. I was able 
to do this using google chromes development tools by setting my user agent. This is the fist time I had to do this. The
was also a testament to how much more familiar I would become with the development tools in google chrome. More examples
on that in later front end stories. My next task was to create the dashboard itself. I would have to come back to this 
mobile dashboard to touch it up in a later story which was a struggle for sure. As far as the first part of the 
dashboard was concerned, creating the buttons was an easy task. Below is the code I used for the buttons in the dashboard.

    <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;"></button>

Getting the buttons aliened properly up was another story. In general, I found getting objects on a UI to line up is a
very difficult part of front end work. Below is the code I wrote for the initial incarnation of the mobile dashboard.
This organization worked on the mobile display I for the iPhone X that I was using but would later have to be changed to
accommodate other mobile displays. 

    @if (User.IsInRole("Employee"))
    {
        <div class="btn-toolbar " role="toolbar" aria-label="Toolbar with button groups">
            <div class="btn-group" role="group" aria-label="First group">
                <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;">
                    @Html.ActionLink("My Jobs", "Index", "Jobs")
                </button>
            </div>
            <div class="btn-group" role="group" aria-label="Second group">
                <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;">
                    @Html.ActionLink("Company News", "Index", "CompanyNews")
                </button>
            </div>
        </div>
        <br>
        <div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
            <div class="btn-group" role="group" aria-label="Third group">
                <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;">Chat</button>
            </div>
            <div class="btn-group" role="group" aria-label="Fourth group">
                <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;">
                    @Html.ActionLink("Manage Account", "Index", "Manage", routeValues: null, htmlAttributes: new 
                    { title = "Manage", Style = "color: White;" })
                </button>
            </div>
        </div>
    }
    
Because the website was not prepared to accommodate mobile users, after this task was complete I had to make a few more 
changes to the mobile dashboard to integrate the design of the websites media. Primarily, this was making sure the 
dashboard had the background banner visible. Initially, there was just a giant block of whitespace above the dashboard.
After I looked into the cause a bit more, I found this block of code in the dashboard controller file.

      @if (Request.Url.PathAndQuery != "/" || Request.Url.PathAndQuery != "/Dashboard/")
    {
        //checks if the user is not the home page if they are not on the home page, the banner
        //is assigned the construction id which has a @media rule to not show the image if
        //the screen is smaller than 600px
        <div class="ei-banner">
            <div id="construction">
                <img src="~/Content/img/home-banner.jpg" />
            </div>
        </div>
    }
    else
    {
        //if the user is on the home page, there is no id tag meaning the banner will show
        <div class="ei-banner">
            <img src="~/Content/img/home-banner.jpg" />
        </div>
    }
    
This was the block of code I had to modify to make the banner visible, since the media rule was preventing it from being
shown. Below is the updated code I wrote to do this. You will see that I only wanted the banner to be displayed in the
mobile dashboard reflected in the code. The comments in the also give context to any user unfamiliar with the code.

      @if (Request.Browser.IsMobileDevice && Request.Url.PathAndQuery.StartsWith("/Dashboard/"))
    {
        //Checks if the user is on a mobile device and is on the dashboard page. If this is the case
        //it will render the home banner on the mobile dashboard page.

        <div class="ei-banner">
            <img src="~/Content/img/home-banner.jpg" />
        </div>
    }
    else if (!Request.Browser.IsMobileDevice)
    {
        //if the user is not on a mobile device, the home banner will be rendered on all pages.
        <div class="ei-banner">
            <img src="~/Content/img/home-banner.jpg" />
        </div>
    }
    
##### The Problem #3

My next front end story was the second largest and second most challenging. We were selecting a new background image 
for the website and need to restyle every page according to that photo. The first issue I ran into was trying to resize 
the new photo and not have it look awkward or stretched on the page. 

##### The Solution #3

This is when I really started using Chromes developer tools in a way that I had not before. Since the photo that was
selected was the same that the company used for it's actually website, I used the companies website as a reference for
how to write my code. I spent some time in developer tools studying their css and html trying to make it fit into our
already existing code. In the end the css code block that I need was simple. That code is presented below.

    .ei-banner {
    position: relative;
    width: 100%;
    display: table;
    table-layout: fixed;
    }
    
The next step was to restyle the entire website according to that photo. Choosing the colors was fun and simple. That
was also done with the color picker on Chromes developer tools. Dev tools made it super easy to test out color schemes 
on different pages. Once I realized that all of the colors I had to restyle were defined in our bootsrap.css I had to 
determine a way to change them. After a bit of researched I learned that it was best to create a custom css file 
instead of changing the bootstrap.css. I learned that in order to overwrite the bootstrap I had to be sure the custom 
css file was targeting the same name as the bootstrap.css. From that point, I referenced dev tools to determine what
bootstrap css was effecting what component I wanted to overwrite. 

After I had the whole file writen I realized that in the event any of these colors wanted to be changed in the future, 
it would be tedious to go through the entire file and change each color one by one. After a bit of researched I learned     
that I could make css variable that I could reference instead just writing the colors. Below is a code block 
demonstrating how that was done. 

    :root {
    --dark-brown: #5b4e50;
    --light-grey: #d7ddde;
    }
    body {
        color: var(--dark-brown);
    }
    .panel-default > .panel-heading {
        color: var(--light-grey);
        background-color: var(--dark-brown);
    }
    

There were times when I needed to apply a color to the text inside a button link that had no way of targeting it. After
a bit of research, I found an overload for the html.Actionlink function that allowed me to give a css target to the 
text. An example of that code is listed below.

     <button type="button" class="btn btn-info btn-md mobileDashboardButton">
        @Html.ActionLink("My Jobs", "Index", "Jobs", null, new { @class = "dashBoardLink" })
     </button>


##### The Problem #4

This story was my last one of the front end sprint and was the most challenging of the bunch. I had to make sure the 
mobile dashboard layout stayed consistent regardless of the mobile device being used. This required to take a look back
at the code I had initially writen to determine how to do this. I had to find a way to make the mobile dashboard more 
responsive.

##### The solution #4

I tried several different combinations of code outside of my initial code. Eventually I settled on a basic layout using
bootstraps row class. That code block is listed below. I'll as context to the rest of the code in that block 
momentarily.

    <div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
        <div class="row mobileDashboardRow">
            <button type="button" class="btn btn-info btn-md mobileDashboardButton">
                @Html.ActionLink("My Jobs", "Index", "Jobs", null, new { @class = "dashBoardLink" })
            </button>
            <button type="button" class="btn btn-info btn-md mobileDashboardButton">
                @Html.ActionLink("Company News", "Index", "CompanyNews", null, new { @class = "dashBoardLink" })
            </button>      
        </div>
        <div class="row mobileDashboardRow">      
            <button type="button" class="btn btn-info btn-md mobileDashboardButton">
                @Html.ActionLink("Mobile Chat", "MobileChat", "ChatMessages", routeValues: null, htmlAttributes: new 
                { @class = "dashBoardLink" })
            </button>
            <button type="button" class="btn btn-info btn-md mobileDashboardButton">
                @Html.ActionLink("Manage Account", "Index", "Manage", routeValues: null, htmlAttributes: new 
                { @class = "dashBoardLink" })
            </button>
        </div>
    </div>
    
The next step was a bit more involved. Since I had to accommodate a number of different mobile displays, I had to create
several different media rules in css to achieve this. This part required a lot of trial and error. You'll notice in the
code snippet below, initially I had defined a lot of the css styling directly in the cshtml file. This would have to 
change in order for me to make the code work with every mobile display. In the code block above, you'll see that I added
very specific classes to the row call "mobileDashboardRow" and to the button called "mobileDashboardButton". This
allowed me to target with my css without overwriting the "row" or "button" class in bootstrap, which might effect the 
whole project.

    <div class="btn-group" role="group" aria-label="First group">
        <button type="button" class="btn btn-info btn-lg btn-block" style="width: 170px;">
            @Html.ActionLink("My Jobs", "Index", "Jobs")
        </button>
    </div>
    
In the code below, you'll see where I applied a number of media rules to accommodate each mobile device. After some 
trial and error, I was able to settle on a layout that would be both aesthetically pleasing and user friendly.


    @media (max-width: 330px) {
        #nav-brand {
            font-size: 25px
        }
        .mobileDashboardRow {
            width: 310px
        }
        .mobileDashboardButton {
            width: 130px;
            height: 50px;
            margin: 10px 10px 10px 10px;
            font-size: 13px;
        }
    }
    @media (min-width: 360px) {
        .mobileDashboardRow {
            width: 340px
        }
        .mobileDashboardButton {
            width: 150px;
            height: 50px;
            margin: 0 10px 20px 10px;
            font-size: 16px;
        }
        .mobileDashboardButtonBottom {
            width: 150px;
            height: 50px;
            margin: 10px 10px 0 10px;
            font-size: 16px;
        }
    }
    @media (min-width: 700px) {
        .btn {
            white-space: normal;
        }
        .mobileDashboardRow {
            width: 400px
        }
        .mobileDashboardButton {
            width: 150px;
            height: 100px;
            margin: 0 20px 40px 20px;
            font-size: 25px;
            border-radius: 20px;
        }
    }
    @media (min-width: 900px) {
         #nav-brand {
            font-size: 35px
        }
        .mobileDashboardRow {
            width: 550px
        }
        .mobileDashboardButton {
            width: 200px;
            height: 140px;
            margin: 30px 30px 0 30px;
            font-size: 35px;
            border-radius: 20px;
        }
    }
