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

The solution cannot be used standalone. As minimum it needs to be fed with data for six of the parameters of the PE header of the protable file. Further it can be implemented  as input to IT defensive systems like Firewall, IPS, etc. It can be integrated within a larger cyber security system placed in any IT infrastructure (from a single computer to a large scale IT network). It can work (as part of larger cyber security system) independantly from humans, drawing their attention only when harmful code is about to be executed within the secured IT system. Natural user of it are IT security experts within the CISO team.

Images will make your README look nice!
Once you upload an image to your repository, you can link link to it like this (replace the URL with file path, if you've uploaded an image to Github.)
![Upload_image](https://github.com/omnitel1113/my-new-project/blob/main/upload%20image.png)


The code of my NN:
```
import numpy as np

dataset = open("subset 6 parameters 4355.csv", "r")
Header = dataset.readline()
#print(Header)

I = dataset.read()
Ilist = I.splitlines() # split the input features in lines - each line has the features of one training or testing file
Olist = []
for i in range(len(Ilist)):
    m = Ilist[i].split(",") # form list of each set of fetures for a file
    Olist.append(m[0]) # put the class column in separate list
    m = m[1:] # take out the first (class - which shows malware or legit file) column and form features dataset
    Ilist[i] = m
# make train and test data numpy arrays
split = input("How would you like to split the dataset for training and for testing? Usually 10% are committed for testing. Please input integer for testing: ")
print()
x_train = np.array(Ilist[:-int(split)], dtype = float)
x_test = np.array(Ilist[-int(split):], dtype = float)
dataset.close()            
y_train = np.array(Olist[:-int(split)], dtype = float)
y_test = Olist[-int(split):]
y_test = [int(i) for i in y_test]

#linear regresion, least squares calculation
c = np.linalg.lstsq(x_train, y_train, rcond = None)[0]
#print(c, "is c") 
y_predict = (x_test @ c).tolist()
y_step = []
for j in range(len(y_predict)):
    if y_predict[j] < 0.5:
        y_step.append(0)
    else:
        y_step.append(1)

#compare prediction/least squares method with real values for legit/malicious files
o = 0
for k in range(len(y_test)):
    if y_test[k]-y_step[k] != 0:
        o +=1

#nearest neighbours method

def dist(a, b): #define distance between two elements of two 1d np.lists
    sum = 0
    for ai, bi in zip(a, b):
        sum = sum + (ai - bi)**2
    return np.sqrt(sum)

k = int(input("Please define the number of nearest neighbours to calculate the distance from them: "))

for i, test_item in enumerate(x_test):
        # calculate the distances to all training points
        distances = [dist(train_item, test_item) for train_item in x_train]
        D = list(np.sort(distances))
        Dk = D[:k]
        y_nearest = []
        for j in range(len(Dk)):
            nearest_indices = distances.index(Dk[j])
            y_nearest.append(y_train[nearest_indices])
        y_predict[i] = int(np.round(np.mean(y_nearest)))

#compare prediction/nearest neighbours with real values for legit/malicious files

p = 0
for t in range(len(y_test)):
    if y_test[t]-y_predict[t] != 0:
        p +=1
#print(y_test, "y_test")
print()
print(o, "differences out of", len(y_test), "comparisons by linear regression and least squares method.")
print(100*o/len(y_test), "% difference with linear regression and least squares method.")
#print(y_step, "prediction with linear regression and least squares method.")
print()
print(p, "differences out of", len(y_test), "comparisons by nearest neighbours method with", k, "nearest neighbours")
print(100*p/len(y_test), "% difference, with nearest neighbours method.")
#print(y_predict, "prediction by nearest neighbours method.")


```


## Data sources and AI methods

I used the dataset gathered by another GitHub fellow - Dr. Ajit Kumar from Pondicherry University, India:
[GitHub](https://github.com/urwithajit9/ClaMP).
I took a subset of it with 4355 samples of different portable execution files' PE header parameters (out of his 5185). For each sample I took 6 parameters from the PE header - E_file (file entropy), CreationYear, SizeOfInitializedData, DllCharacteristics, MajorImageVersion, CheckSum. The decision to process these parameters was based both on the observation of Dr. Ajit Kumar and the research paper of Yibin Liao from The University of Georgia, Athens, USA:
[UGA](http://cobweb.cs.uga.edu/~liao/PE_Final_Report.pdf).

The NN uses sequentially two methods for classification - linear regression with least squares method and nearest K neighbours method. The second method generally behaves better with about 5% better success ratio. Approximately 20% false results (positive and negative) against ~ 25% with the linear regression.

## Challenges

1. The proposed NN is having comparatevily high number of false positives (~11%) and false negatives (~15%), based on it linear regression method with test set of 400 and train set of 3995 sets of input features. Reason to me is that the NN is simple single layer only network which is not suitable to use when the data shows non-linear characteristics. I think that adding additional hidden layer/s will improve considerably its classification performance but currently cannot figure out the implementation of the hidden layers, their activation functions and weights toward the next level.
2. Choosing just 6 out of 55 parameters of the PE header to me also deprives the NN of abilities to make good decisions. More observation need to be done on the differences between rest 49 parameters in legitimate and malicious portable files.

## What next?

1. Addressing the challanges from the previous section to me are the immediate necessity for help to improve the system considerably.
2. Expanding the capabilities of the NN to inspect not only portable files will give great new value of it. For this probably quite different parameters must be considered and gathered which could be the long term objective of the project.


## Acknowledgments

My biggest source of inspiration was University of Helsinki and its Reaktor courses - Introduction to AI and Buiding AI.
Also without the works mentioned in the section "Data sources" the current status of the project could not be possible. 
