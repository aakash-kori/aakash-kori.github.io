---
layout: post
title: 'Summary: "What nobody tells you about documentation"'
category: "notes"
tags: ["writing", "documentation", "programming"]
desc: This article tries to summaries "What nobody tells you about documentation"
---
The article ["What nobody tells you about documentation"](https://www.divio.com/blog/documentation) details on how to write documentation for program. This article aims at providing details of different types of documentation, their intent, content, scope and purpose. This simplifies the documentation process by helping writer have right mindset while documenting. 

# Types of Documentation
1. Tutorial 
    - example: readme
    - level: beginner
    - orientation: learning    
    - purpose: practical + studying
    - dos: 
        - doorway to your software for any user (setup/installation should be included)
        - multiple tasks (task: short set of steps)
        - should have simple achievement tasks(rewarding experience) 
        - should work 100% (induce confidence in software
    - do nots:
        - need not use best practice if not required (complicates process)
        - do not explain beyond what is required (makes tutorial long) 

1. How to guides
    - example: how to fetch x information    
    - level: intermediate
    - orientation: goal    
    - purpose: practical + working
    - dos:
        - should be working (can be part of test-cases)
        - should have proper heading (possible search phrase)
        - should setup/installation (intermediate level) 
        - should be flexible (include small variation)
    - do nots:
        - should not explain more (link to api documentation) 

1. Explanation
    - example: api documentation 
    - level: experienced    
    - orientation: technical understanding 
    - purpose: theory + studying 
    - dos:
        - should be code based (auto generate is better)
        - example if required (for edge case which is difficult to describe) 
        - consistent structure (helps reading)
    - do nots:
        - should not explain about design decision (explain what code does, not why)
        - should not be goal oriented (put it in how to guide)

1. Reference 
    - example: readme
    - level: advanced expert    
    - orientation: information     
    - purpose: theory + working
    - dos:
        - should/can include 
            - discussions
            - design decision (including alternatives) 
            - historical reasons
            - good practices
