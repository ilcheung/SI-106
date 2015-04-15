# SI-106
Restful API-airport data
The following will be the porblem set quesiton to retrieivng airport data

## PS 10

## Ilene Cheung

# import statements
import requests
import json

# This is a function we've provided for you so you can print stuff in a pretty,
# easy-to-read way. 
def pretty(obj):
    return json.dumps(obj, sort_keys=True, indent=2)

## Mechanics: user-defined types, and thinking about them

# [PROBLEM 1]

## We'll go through the process of defining a class to describe a photograph on Flickr.
## We've provided some of the information filled in for this first example.
## Then you'll complete the same structure on your own for a different type of thing.

# The following exercises are a thought exercise to help you think about how you would
# define a class to represent a flickr photo.

# The name of your class will be... 
new_class_name = "Photo"

# An instance of the class will represent one
represents = "photograph on flickr"

# The Photo class should have how many instance variables?
# Let's say you want each Photo to have: a title, an author, and a list of tags.
num_instance_vars = 3 # when you decide this, 
					  # you have to think about what attributes you want to keep track of!

# One method of your class, other than __init__, will be named:
one_class_method = "display_info"

# When invoked, that method will...
method_description = "display all the info about the photo for the user, like the title, author, tags"
also = "There may also be other methods of this class"

total_string = """
The name of my class will be %s. One instance of the class will represent one
%s. The class will have %d instance variables. One method of my class, other 
than __init__, will be named %s. When invoked, that method will 
%s. %s.
""" % (new_class_name, represents, num_instance_vars, one_class_method, method_description, also)
# this line will print out the above paragraph with the information provided above filled in.
print total_string

### Now, do this again by yourself for a car. If you were to define a car class, 
### what might you pick for instance variables and methods?
# The name of your class will be... 
car_class_name = "" 
# An instance of the class will represent one
reps = ""
# The class should have how many instance variables?
num_inst_vars = 0
# Write comments noting what some instance variables could represent below -- at least three.
# 1.
# 2.
# 3.

# One method of your class, other than __init__, will be named...
# Think: anything you want a car to do. 
#  Change license registration and print something out? Drive forward? 
car_class_method = ""

# When invoked, that method will...
# (Think: How would you represent this method you named above in code or in text 
# for someone to see in a program? 
# Look at the examples given in the textbook and the flickr Photo class above.) 
car_method_description = ""

car_str = """The name of this class will be: %s. So you are creating a type %s.
An instance of the class will represent one %s. It should have %d instance
variables. One method of this class will be called %s, which 
will %s.
""" % (car_class_name,car_class_name,reps,num_inst_vars, car_class_method, car_method_description)
print car_str

#####

## Making a tag recommender, using the Flickr API!

# [PROBLEM 2] - Multi-part

# In this problem, we'll walk you through steps you need to take to make a tag
# recommender, but we won't be providing you code. You'll use the documentation
# we'll copy in here, and the code you've seen in lecture to deal with Flickr
# and other API requests, to translate the English into Python and make your 
# program work.
# Go through step by step. You may want to look back at Problem Set 9 
# to remind yourself of the steps to go through when dealing with APIs 
# and making requests for data, and Problem Set 6 and Hackpad exercises 
# can remind you of how to deal with nested data.
# HINT: the flickrREST function will be very helpful for the rest of the question
###
flickr_key = "" # paste your flickr key here
Apply for an API key https://www.flickr.com/services/api/misc.api_keys.html

# Useful function definitions 
def flickrREST(baseurl = 'https://api.flickr.com/services/rest/',
    method = 'flickr.photos.search',
    api_key = flickr_key,
    format = 'json',
    extra_params={}):
    d = {}
    d['method'] = method
    d['api_key'] = api_key
    d['format'] = format
    for k in extra_params:
        d[k] = extra_params[k]
    return requests.get(baseurl, params = d)

## Here's another example call to flickrREST below -- note that you have to pass in
## a new params dictionary to get the parameters/param values you want in your request!
## uncomment the following line to try it out, or edit it, to think about how you
## can make a call to this function like you've done already, and how/why you might 
## make a different call to this function.

#print flickrREST(extra_params = {'tags':'mountains', 'per_page':10}).url

## Remember that for the Flickr API, you have to remove the bit at the beginning and end
## that isn't json: "jsonFlickrApi("" at the beginning, and ")" at the end.
## So once you get a response string, use this function to do that, to get a response string that
## you can pass to json.loads():
def fix_flickr_resp(response_string):
	return response_string[len("jsonFlickrApi("):-1]

## Let's start making the tag recommender! This has several steps.
## HINT: Thinking about the process from PS 9, the Flickr examples, and 
##       the structure we went through in section last week, will help!

# 1) Ask the user to input a tag.

# 2) Use the tag you got from part one in an API call to Flickr to get back 50 photos that 
#	 have that tag.

# 3) Extract each of the photo ids from that response, making a list of all of them.

# 4) For each of the photo ids, make a request to the flickr API using the 
#    method flickr.photos.getInfo (this is like the default method used in flickrREST: flickr.photos.search)
#    -- the method describes the place to go to get the data within the flickr service
#    See documentation at https://www.flickr.com/services/api/flickr.photos.getInfo.html
# Once you are done, try pretty prining the id of the first photo. This will help you for the next part of the question. 


# 5) Extract the tags used on each photo, and accumulate frequencies 
#    with which each tag occurs across all those photos you found when you searched.

# 6) Output (print, for the user to see) the five tags (other than the searched on tag)
#    that were used most frequently. HINT 1: take a slice of the sorted list.
#    HINT 2: skip the first element in the sorted list. That will be the tag
#    the user typed in, since all the photos have that tag.

