#Building AI course project
<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# Project Title

A Neural Network that classifies portable files into legit or malicious based on features in their PE headers.

## Summary

The project is to build a Neural Network (NN) which examines six out of fifty-five parameters in the PE header of a portable file. Based on the values and combinations of these parameters supplied to the NN it outputs its prediction for the class of the file - 0 is legitimate class, 1 is malicious class.


## Background

Deliberate penetrations and infections of IT systems by malicious hackers is serious and growing problem. The attack techniques become more sophisticated and their number rises every day. Today, the signature based anti virus programs although quite advanced cannot always cope with the problem. They perform great on hash signatures of known attack vectors but are poor when meeting new, not yet discovered and/or published threats (so called zero day attacks). Furthermore the anti virus programs rely on the timely manner in which the users and/or administrators of IT networks update the libraries for known viruses. If an update is missed the IT system becomes vulnerable to latest threats. Therefore the science and industry in parallel are proposing other methods for cyberdefense. In general these methods give their decision based not so much on the existance or not of the inspected code in a antivirus library, but on other attributes of the code as for example its parameter characteristic fields, its communication to external entities, its behaviour, etc.  An experienced cyber analyst can easily detect strange and harmful behaviour of certain piece of code, but even she/he will be in trouble when chasing it in a large IT system or coping with many malicious codes at one and the same time. The depicted problem is quite common and frequent. Myself being an integrator of cyber security systems face such challanges quite often. To me the solution is to use AI systems which could become an indispensable assistant to IT security experts and my motivation to open the project is to try to address a tiny portion of the enormous cyber defense domain.


## How is it used?

Describe the process of using the solution. In what kind situations is the solution needed (environment, time, etc.)? Who are the users, what kinds of needs should be taken into account?

Images will make your README look nice!
Once you upload an image to your repository, you can link link to it like this (replace the URL with file path, if you've uploaded an image to Github.)
![Cat](https://upload.wikimedia.org/wikipedia/commons/5/5e/Sleeping_cat_on_her_back.jpg)

If you need to resize images, you have to use an HTML tag, like this:
<img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Sleeping_cat_on_her_back.jpg" width="300">

This is how you create code examples:
```
def main():
   countries = ['Denmark', 'Finland', 'Iceland', 'Norway', 'Sweden']
   pop = [5615000, 5439000, 324000, 5080000, 9609000]   # not actually needed in this exercise...
   fishers = [1891, 2652, 3800, 11611, 1757]

   totPop = sum(pop)
   totFish = sum(fishers)

   # write your solution here

   for i in range(len(countries)):
      print("%s %.2f%%" % (countries[i], 100.0))    # current just prints 100%

main()
```


## Data sources and AI methods
Where does your data come from? Do you collect it yourself or do you use data collected by someone else?
If you need to use links, here's an example:
[Twitter API](https://developer.twitter.com/en/docs)

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

## Challenges

What does your project _not_ solve? Which limitations and ethical considerations should be taken into account when deploying a solution like this?

## What next?

How could your project grow and become something even more? What kind of skills, what kind of assistance would you  need to move on? 


## Acknowledgments

* list here the sources of inspiration 
* do not use code, images, data etc. from others without permission
* when you have permission to use other people's materials, always mention the original creator and the open source / Creative Commons licence they've used
  <br>For example: [Sleeping Cat on Her Back by Umberto Salvagnin](https://commons.wikimedia.org/wiki/File:Sleeping_cat_on_her_back.jpg#filelinks) / [CC BY 2.0](https://creativecommons.org/licenses/by/2.0)
* etc
