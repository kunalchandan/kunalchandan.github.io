---
title: Tesla SRE Interview
# date: 2023-06-15 14:00:00
categories: [interviews]
tags: [interview, tesla, software]
author: kchandan
math: true
---

# Panel Interview Prep
Chill chat with Daniel Arias
- Getting info about compensation etc.
- Software Engineering role or Site Reliability Engineer role
- Jeremy liked my last interview/round 1 technical
- Gonna be working on factory software
  - Working with Technical PMs
  - Manufacturing processes
  - Working on Model Y and CyberTruck
- Director Nagesh
- Jeremy's boss AD, aydee?

Next round:
- Topics:
  - Databases
  - SDLCs
  - System Design

- Freeform sort of questions about the rest
- 3-4 interviewers for the next round
- Same structure as last interview
- GoLang would be ideal
- Jeremy joins last 30 minutes
  - Post interview
  - Jeremy won't be on the meeting

Preferred interview for 1 week from now on Thursday or Wed/Fri

Asked about TN visa process.

Receiving immigration assessment.


Timeline:
- ASAP
- Cannot extend offer until the first week of July
- After headcount review

Compensation levels:
- Targeting high P3 most likely P2
- Can exercise stock after 4 years
- Yearly review for compensation
- Vest stock yearly
- $5000 for P2 relocation, after tax, no receipts required

# Panel Interview

## Interviewer 1 - Paul Leimer
pleimer@tesla.com
Asked question about containers:

During the question we want the container objects to store a location and a mapping of objects and their counts as well as a reference to some number of sub-containers that you can add to a parent container.

The following functions were requested to be implemented:
- Add a container to a parent container
  - Just gets added to a list of containers
- Move a container (and sub containers to a location)
  - Be sure to recursively call move container so all sub-containers are moved
- Remove a container from a parent container
  - Maintain a reference to a parent container and remove the container that way

Implementation was completed with 1.5 minutes to spare. Asked to write some test, but that just wasn't enough time.

## Interviewer 2 - Ganesh Kurcheti
jalkarawi@tesla.com




```
# [8,9,10] n=1
# [8,9,10]


array = [1, 2, 5 ,0 ,1, 7,3]
n = 3


# print(sorted(array)[n:])

array = [1, 2, 5 ,0 ,1, 7,3]
[0,1,7,3]
[5,0,1,7]
n = 3

i = 0
while i < n:
    if array[0] < array[len(array)-1]:
        array = array[1:]
    else:
        array = array[:len(array)-1]

    i += 1

print(array)
  A : "HAI" 10
  A: "test" 11
  B :"hAIL" 11
  B: "test" 13
  b: "test" 14

  10,12

for message in messages:
    if message outside of range
        discard

# O(n)

for message in messages:
    count is done per user
    hyperloglog count uniq number of messages each user sends

# O(n)

sort the counts per user

# O(u log u)
```

## Interviewer 3 Jhilan Alkarawi
jalkarawi@tesla.com
- Brief intro

Create a tree from a list of nodes.
```
from functools import reduce
import operator
def all_reduce_logical_or(lst):
    return reduce(operator.or_, lst)


input_data = [{
    "ParentId": None,
    "Id": "a",
    "Children": []
},
{
    "ParentId": "a",
    "Id": "b",
    "Children": []
},
{
    "ParentId": "b",
    "Id": "d",
    "Children": []
},
{
    "ParentId": "d",
    "Id": "g",
    "Children": []
},
{
    "ParentId": "a",
    "Id": "c",
    "Children": []
},
{
    "ParentId": "c",
    "Id": "e",
    "Children": []
},
{
    "ParentId": "c",
    "Id": "f",
    "Children": []
}]

def insert(node, child):
    if child["ParentId"] == node["Id"]:
        node["Children"].append(child)
        return True
    else:
        for subNode in node["Children"]:
            res = insert(subNode, child)
            if res:
                return True
        return False


def try_inserting(sub_data):
    for data in sub_data:
        if data["ParentId"] == None:
            output_data["Children"].append(data)
            sub_data.remove(data)
        else:
            inserted = insert(output_data, data)
            if inserted:
                sub_data.remove(data)


output_data = {
    "ParentId": None,
    "Id": None,
    "Children": []
}

def main():

    while len(input_data) > 0:
        try_inserting(input_data)

print(output_data)


# //         a
# //        b  c
# //      d   e  f
# //    g

# =========================== input =================================

#         [
#             {
#                 "ParentId"": None,
#                 "Id": "a",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "a",
#                 "Id": "b",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "b",
#                 "Id": "d",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "d",
#                 "Id": "g",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "a",
#                 "Id": "c",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "c",
#                 "Id": "e",
#                 "Children": []
#             },
#             {
#                 "ParentId"": "c",
#                 "Id": "f",
#                 "Children": []
#             }
#         ]


# =========================== output =================================


#         {
#             "ParentId"": null,
#             "Id": "a",
#             "Children": [
#                 {
#                     "ParentId"": "a",
#                     "Id": "b",
#                     "Children": [
#                         {
#                             "ParentId"": "b",
#                             "Id": "d",
#                             "Children": [
#                                 {
#                                     "ParentId"": "d",
#                                     "Id": "g",
#                                     "Children": []
#                                 }
#                             ]
#                         }
#                     ]
#                 },
#                 {
#                     "ParentId"": "a",
#                     "Id": "c",
#                     "Children": [
#                         {
#                             "ParentId"": "c",
#                             "Id": "e",
#                             "Children": []
#                         },
#                         {
#                             "ParentId"": "c",
#                             "Id": "f",
#                             "Children": []
#                         }
#                     ]
#                 }
#             ]
#         }
```