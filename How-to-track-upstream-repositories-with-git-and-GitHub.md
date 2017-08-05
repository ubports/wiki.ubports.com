## Prolog
Okay this might put a smile on a lot of faces, but guess what, until last year I had no idea about how git and GitHub are working.

In my company and for private things I used svn, and I found git obscure, overloaded with features and in general too much effort to learn.

That has changed a lot now. And the primary reason was? Right, UBports and the necessary workflow when working with people you dont know, and they don´t know you in turn. Because when there is no full trust between all the people participating in a huge distributed software project, it is necessary to prevent accidential or intentional damages. And believe me, SVN for example is really hard to repair, if someone did some nice accidental commit, or delete.

In theory, any RCS saves you from lost data. But its a matter of time and effort sometimes to clean up after aome accident has happened, and we had quite a few times in my company, and it wasted hours.

So there is now git, and because it is a distributed RCS it has a few unique features (not unique on the planet but in comparison with centralized RCS. Bazaar for example does the same as git, feature-wise).

## Why we use git?
A good part of the question is above in my personal statement, but here are the more general properties:

* a distributed RCS allows all users to create and delete their local/private branches without disturbing others.