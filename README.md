# Update the updater

WordPress updates for Core, plugins, and themes are based on a number of Core classes:
- https://developer.wordpress.org/reference/classes/wp_upgrader/
- https://developer.wordpress.org/reference/classes/core_upgrader/
- https://developer.wordpress.org/reference/classes/theme_upgrader/
- https://developer.wordpress.org/reference/classes/plugin_upgrader/

Alongside these main classes are several other update-related classes and functions, including those for updating translations.

The ability to manually update WordPress from the admin area, and to install and update plugins and themes, has existed since 2.3 in 2007. Auto-update features were added in WordPress 3.7 (for minor releases), extended in 5.5 (as opt-in for plugins and themes), and 5.6 (major releases).
To make the user experience of auto-updates even better, and build trust with users and extenders, it's important that this mechanism works well and provides all the failsafe checks needed.

The WordPress Core update has proven to be generally reliable, but it doesn't actually have many tests nor is well documented. There are also some reliability concerns around adding new files and the overall number of changed files, which is the reason WordPress currently tries to [keep the number of changed files in minor releases to a minimum](https://make.wordpress.org/core/2017/03/11/continuing-inline-docs-improvements-adjacent-to-4-8/#comment-32248).
Plugins and themes updaters are older: in general, all of them can be improved.
As one of the most widely used plugins in the WordPress ecosystem, we have experienced some pains related to these processes so decided to actively work on this issues. We believe that other plugin and themes authors have gone through the same experiences and we hope they will join us in this effort of updating the updater.

## What are we working on
- We are combing through Trac to find all open tickets: start with Core, then move to Plugins and eventually Themes
- We are reviewing all the classes involved to make sure their code is efficient and if there is room for improvement

## What are the next steps
This is a big project, one that can help other thousands of companies, so I hope you will join us in the effort.
We have created a GitHub repository under our company account. There, you will find a project board where we are documenenting and managing all we are doing. 
Once the reasearch part is over, and the steps to take to improve the updaters are clear, we will start weekly meetings in #core or a dedicated channel.

## Timeline
5.7 - Reaserch and proposal phase
5.8 - Coding and documenting 
