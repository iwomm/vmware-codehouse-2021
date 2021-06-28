# VMware CodeHouse 2021

This project will serve as guidance for attendees and mentors of VMware CodeHouse 2021.

The goal of VMware CodeHouse 2021 will be to create an application that furthers STEM eduction and/or Diversity & Inclusion.

This project contains several chapters with hands-on coding exercises. Each chapter adds new code to the last one. A chapter is broken down into a few small steps, with each step introduces a bite-size new concept or one tool. The expected code result for each chapter is provided in the `codehouse-2021-prework` sub-folder inside the chapter's folder. The finished product off the last chapter is a TODO web application written in Go, Gin and Vue. 

Table of content for the hands-on exercises:
- Chapter 1 - Set up development tools, create the "Hello Go & Gin" app
- Chapter 2 - Create the Rest API in Go & Gin
- Chapter 3 - Scaffold the "Hello Vue" app
- Chapter 4 - Connect the Vue App to the API
- Chapter 5 - Polishing and clean up

There are to main components in the finished app:
- **Server side** -  a Rest API written in Go (the base language) and Gin (a web framework for Go).
- **Client side** -  a Javascript application running in the browser that interacts with the API. Vue is the client-side Javascript framework.

Given the step-by-step nature of the chapters, you can jump right into chapter one and start learning by coding. If you find some concepts demanding more introduction, use the recommended readings below to get an overview of a subject and come back to coding. The recommended readings were selected for their brevity and clarity in order to save learning time.     

## Recommended reading

To make sure you are comfortable with the concepts and tools we will be using, please read through the following documents well in advance:

- Introduction to **Go**. [Learning Go](https://www.miek.nl/go/) is one online free book featuring numerous execises. There are [many resources for learning Go](https://github.com/dariubs/GoBooks).
- Intruduction to **Rest API**. [This page ](https://www.sitepoint.com/rest-api/)covers many aspects of Rest API with simple exercises.
- Introduction to **Gin**. [This tutorial ](https://blog.logrocket.com/how-to-build-a-rest-api-with-golang-using-gin-and-gorm/)builds a simple CRUD API using Gin. It uses Sqlite for database. 
- Introduction to **Vue**. [A turtorial for Vue like this one](https://www.taniarascia.com/getting-started-with-vue/) provides a good overview of the concepts and will make you feel more comfortable working with Vue.
  
## Completion of pre-req tasks

Once you have completed these tasks, make a pull request to this repository with a Markdown file in this format:

`[initials of your first and last name].md`
```
I've finished reading through the pre-req docs and ran the final result on my laptop!
```
