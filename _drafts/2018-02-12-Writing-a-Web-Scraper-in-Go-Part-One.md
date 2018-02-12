---
layout: post
title: "Writing a Web Scraper with Go: Part One"
description: How to scrape a website with Go
---

### Introduction

This post is part one of an eight part series on how to scrape a website in Go and store specific data in Firestore. The first three parts will focus soley on setting up a web scraper in Go. Once we have acquired the data we want to save, we will be able to store it in a Firestore database. This enables us to do the following:  
  	&emsp;1. Acquire information from a website  
  	&emsp;2. Store it in Firestore in our own custom data structures  
  	&emsp;3. Efficiently query Firestore across various supported platforms such as Android, iOS (Swift or Objective-C), Python, or Node.js.

By the end, you will be able to use Go and Firestore to create your own API for any website.

### Environment Setup

I will assume that you are starting from ground zero. In order to setup your environment, you need to first get an editor. I recommend either [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](https://www.sublimetext.com/). Next, install the relative plugins for Go. If you chose Visual Studio Code, open the Extensions tab on the left side of the editor, search Go, and install the first extension by lukehoban. If you chose Sublime Text, install Package Control and then install the package GoSublime [by following this guide](http://www.techinfected.net/2017/06/install-and-use-package-control-sublime-text.html). 

After you have a basic editor setup, [download and install the Go programming language](https://golang.org/dl/).

