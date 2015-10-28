# THOR-Mozfest
Building citation lists using ORCID records and DOI metadata at Mozfest 2015

# Aim of the session

We're going to try to get to grips with the Public ORCID API and match identifiers in ORCID records to the metadata held by Datacite and/or Crossref using the DOIs.

Step 0
- Get some API credentials

Step 1
- Get a list of works for an ORCID ID

Step 2
- Get the metadata from the DOIs
- Decide how to deal with non-DOI works, we can get limited metadata from ORCID

Step 3
- Turn the metadata into a reference list

Step 4
- Authenticate users so we can display their works 

Step 5
- Go crazy - work on your use cases
- Make it work for multiple authors - build co-author graphs
- Make it work in the other direction - extract ORCIDs from DOIs
- Add an author search
- Turn the ORCID profile into a widget
- Produce BibTeX
- Work out how to map to RIS or Endnote XML
- Pipe the output into another service or tool
- Enable users to update their profiles, push things into ORCID, use the member API, get sandbox credentials
- ETC!


# The ORCID Public API

The ORCID Public API enables you to do the following things:

- Sign in with ORCID / Get a user's ORCID identifier (these two functions follow the same process)
- Retrieve public data from a user's ORCID record
- Search public ORCID registry data

Using the Public API requires a set of credentials consisting of a Client ID and a Client Secret. You can [configure credentials for the Public API](http://members.orcid.org/api/accessing-public-api) from your personal ORCID account.

There is a great [introduction to using the Public API](http://members.orcid.org/api/introduction-orcid-public-api) in the ORCID API documentation

# The ORCID Member API

The ORCID Member API enables you to do everything the public API can do and in addition:

- Add information to an ORCID record, including:
  - works, 
  - employments
  - education
  - peer reviews
  - bio information, such as alternate names and keywords
- Update information that you previously added
- Delete information that you previously added
- Receive notifications when member records change

There is a great [introduction to using the Member API](http://members.orcid.org/api/introduction-orcid-member-api) in the ORCID API documentation

# Authenticating ORCID users

ORCID uses the OAuth2 protocol for authentication.  This is a user centric authentication mechanism that allows users fine grained control over what third parties can and cannot do with their ORCID record.   It works like this:

- Your website directs the user to ORCID using a specially crafted request containing details of the permissions you would like the user to grant you.  E.g. read or update
- The user authenticates to ORCID, if not already signed in
- The user grants (or denies!) permission to your application
- ORCID redirects the user back to your website with an *authorization code*
- You exchange the authorisation code for an *access token* using the ORCID OAuth API
- You include the access token in any subsequent requests you make

Implementing this in code is easier than it sounds.  

More details can be found in the [ORCID OAuth documentation](https://members.orcid.org/api/oauth2).