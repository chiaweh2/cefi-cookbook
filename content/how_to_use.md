# How to Use the CEFI Cookbook

The CEFI Cookbook aims to provide valuable information to users of varying expertise levels. We encourage users to navigate directly to specific topics and pages as needed. Our goal is to make each topic and page self-contained, providing links to associated resources when prior knowledge is required. A quick breakdown of the resources provided is shown below

(cookbook-resource)=
## What resources are provided
- Introduction to CEFI
- Introduction to regional MOM6
- Computational environment setup for CEFI analyses
- Tutorials on accessing CEFI related data
- Derivation of marine resource related indexes
- Free and light cloud computation


## Basic functions of the CEFI Cookbook
### Searching topic
The search bar, located in the left column, is an extremely effective tool for locating relevant resources in the Cookbook. If you're seeking information on a specific topic or have a particular search phrase, utilizing the search bar should be your initial approach.

The following example shows the search phrase of "regionl mom6"
```{image} ../images/search_bar.png
:alt: cookbook search bar image
:class: bg-primary mb-1
:width: 60%
:align: center
```
The search function is comprehensive, encompassing not only phrases found within the text content, but also those present within code snippets.

### Content tree navigation
The content tree navigation is located on the left side of the page shown below
```{image} ../images/content_tree.png
:alt: cookbook content tree
:class: bg-primary mb-1
:width: 60%
:align: center
```
It offers a comprehensive overview of the entire Cookbook, showcasing the various titles and their connections to the diverse resources we aim to provide, as listed [above](cookbook-resource), for the CEFI Cookbook.

### Content page
The core content of each page is situated in the middle column. Scrolling through this middle column allows you to navigate the primary content. At the top, you'll find three main tools (illustrated in the screenshot below), which are incredibly handy.
```{image} ../images/top_function.png
:alt: cookbook top function bar
:class: bg-primary mb-1
:width: 60%
:align: center
```
#### Free cloud computation
The Cookbook interface, built on the [jupyterbook](https://jupyterbook.org/en/stable/intro.html) platform, offers direct access to lightweight and complimentary cloud computing resources provided by Binder and Google Colab. By clicking on the rocket button (absent if the page doesn't support interactive coding, like this one), a cloud computing session will be initiated in a new tab, presenting a JupyterLab interface when Binder is selected. Please note that the Binder platform may require some time to set up the cloud environment.
```{image} ../images/binder.png
:alt: cookbook binder interface
:class: bg-primary mb-1
:width: 60%
:align: center
```
Google Colab is also an available option, although it may require the installation of additional packages before computations can be executed. 
```{image} ../images/colab.png
:alt: cookbook binder interface
:class: bg-primary mb-1
:width: 60%
:align: center
```
*Binder* is the recommanded choice for accessing the free cloud computation.

(submit-issue)=
#### Submit GitHub issue
On each page, users have the ability to submit a specific issue related to the page they are currently viewing. This feature encourages user contributions and facilitates easy reporting of bugs or suggestions for changes. By leveraging the principles of open science and open-source software, this function keeps the Cookbook as a "CEFI community project".

#### Download for local view
The third functionality allows for the effortless conversion of file formats from an online resource into a locally shareable and downloadable PDF. This feature simplifies the process of transforming digital content into a universally accessible format.

#### Like reading a book
The design concept of the webpage by JupyterBook is to emulate the experience of reading a physical book. It ensures that the bottom of each page consistently features two buttons, leading to the previous and next pages or topics.
```{image} ../images/bottom_page_switch.png
:alt: cookbook page switch button
:class: bg-primary mb-1
:width: 60%
:align: center
```

#### Small content navigation bar in each page
In the rightmost column, a floating content navigation bar is present that moves in sync with your scrolling on the main content. This feature provides a real-time indication of your progress through the content on the page. Furthermore, it streamlines the process of navigating to specific topics within each page by clicking on the floating bar, thereby enhancing user accessibility and ease of navigation.
```{image} ../images/heading_guide.png
:alt: floating navigation bar for each page
:class: bg-primary mb-1
:width: 60%
:align: center
```

## How to make suggestions and participate the development?
We greatly appreciate contributions and feedback, especially on unclear sections and new resources. The most effective way to engage in open discussions and reach the developers of the CEFI Data Portal is by opening an issue or starting a discussion on the GitHub [cefi-cookbook](https://github.com/NOAA-CEFI-Portal/cefi-cookbook) repository or [submit issue for a specific page](submit-issue).
