---
layout: post
title: "Writing a Web Scraper with Go (Part One - Setup Environment)"
description: This post is part one of an eight part series on how to scrape a website in Go and store specific data in Firestore. 
---

### Introduction

This post is part one of an eight part series on how to scrape a website in Go and store specific data in Firestore. The first three parts will focus soley on setting up a web scraper in Go. Once we have acquired the data we want to save, we will be able to store it in a Firestore database. This enables us to do the following:  
&emsp;1. Acquire information from a website  
&emsp;2. Store it in Firestore in our own custom data structures  
&emsp;3. Efficiently query Firestore across various supported platforms such as Android, iOS (Swift or Objective-C), Python, or Node.js.

By the end, you will be able to use Go and Firestore to create your own API for any website. This guide will closely follow my work on *goctftime*, which can be found [on my Github](https://github.com/spitfire55/goctftime).

For part one, I will assume that you are starting from ground zero and have never programmed in Go before. If you are already comfortable with Go programming, you can just:   
&emsp;1. Create a new subdirectory in your GOPATH src directory named *goscrape* with two files: *scraper.go* and *scraper_test.go*.   
&emsp;2. Skip to [Part Two](https://spitfy.re/2018-02-14-Writing-a-Web-Scraper-in-Go-Part-Two).

### Environment Setup

In order to setup your environment, you need to first get an editor. I recommend either [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](https://www.sublimetext.com/). Next, install the relevant plugins for Go. If you chose Visual Studio Code, open the Extensions tab on the left side of the editor, search Go, and install the first extension by lukehoban. If you chose Sublime Text, install Package Control [by following this guide](http://www.techinfected.net/2017/06/install-and-use-package-control-sublime-text.html) and then install the package GoSublime. 

After you have a basic editor setup, [download and install the Go programming language](https://golang.org/dl/). Once your installation is complete, follow the [*Test your installation*](https://golang.org/doc/install#testing) guide to setup your environment and ensure everything is installed correctly. You can optionally complete the [*How to Write Go Code*](https://golang.org/doc/code.html) tutorial by Go (I recommend it, but it's not required for this tutorial).

## Create Project

For this tutorial, we will be building a library to use in multiple projects rather than a single project. In order to do this, we need to create a new folder for our package. I will be using $HOME/go/src/goscrape as my example library and name the package *goscrape*. (**NOTE:** I will be using Unix filepath notation for this tutorial.) If you are confused by what $HOME means, it is a standard environment variable on Linux for the home directory. I will use $HOME to represent my home directory (e.g /home/spitfyre or C:\Users\spitfyre) since it will obviously be different on your system.

Open $HOME/go/src/goscrape in your editor and create a new file named scraper.go. This will be the base file where we setup the basic functionality of our scraper. Create a second file named scraper_test.go. In Go, it is very easy to create tests through the testing library and a simple *go test* command. The details of how this all works is very well explained [in this blog post](https://blog.alexellis.io/golang-writing-unit-tests/). We won't implement testing until Part Two.

### In Part Two...  

In Part Two, we will create the basic skeleton of our web scraper and implement our first unit test.

<div style="text-align:center">
	<a href="https://spitfy.re/2018-02-14-Writing-a-Web-Scraper-in-Go-Part-Two">Go to Part Two</a>
</div>