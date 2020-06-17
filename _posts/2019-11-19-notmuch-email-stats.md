---
layout: post
title: Notmuch email stats
date: 2019-11-19 22:27
categories:
---

I was curious about top 10 email senders for my emails. I use neomutt with
notmuch and this allowed me to perform some nice queries. Here is what I did to
find the top 10 emails senders

Get all addresses notmuch knows about

```bash
notmuch address --deduplicate=address \* > addresses.txt

```

This will extract all emails in the format `Name<foo@bar.com>`

Lets get the just the email part


```bash
notmuch address --deduplicate=address \* | sed -E "s/.*<(.*)>/\1/" > all-addresses.txt
```

Now we can count number of emails sent by these emails addresses


```bash

cat all-addresses.txt | \
  xargs -I% sh -c 'notmuch count from:% and tag: inbox | tr -d "\n"; echo " - %"'

```

The notmuch query is quite flexible which allows to search for specific queries e.g


```bash

cat all-addresses.txt | \
  xargs -I% sh -c 'notmuch count date:"1month..today" and not tag:archive and not tag:starred and from:% | tr -d "\n"; echo " - %"'

```

This will limit the search to all emails within this month and not archived or starred

This query can be slow for large mailboxes. I like to save intermediary results in text files.

```bash

cat all-addresses.txt | \
  xargs -I% sh -c 'notmuch count from:% and tag: inbox | tr -d "\n"; echo " - %"' \
  > addresses-with-count.txt

```

This will print count with email address


```
120 - foo@example.com
1 - bar@example.com
```

We can sort numeric and get the top 10


```
  sort -nr addresses-with-count.txt | head -10
```
