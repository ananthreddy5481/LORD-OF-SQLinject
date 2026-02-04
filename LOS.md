# LORD-OF-SQLinject

#level-1 :

the site is having an sql injection and wanted any user input for completing the level. so give the "or 1=1-- .

#level-2 :

the site needs to have id=admin and the direct input is taken into the query so can give the parameter id='admin' and comment the rest.
#level-3 :

the site also needs to have id=admin but the id has been set already so use the or id=admin( in hex form because the quotes are banned from using) which makes the server to read the id=guest first and then id=admin and as that is a or function there should be atleast conditon true . 

#level-4 :

give the query as ?pw=' || id='admin' and length(pw) > 7-- 
this for knowing the length of the password. 
?pw' || id='admin' and substr(pw,1,1)='0'-- for this query change the center 1 closing into section sign(§) which is the payload-1 that tells about the position of the charecter in the password that is checking and the "0" that is our payload-2 which is the value of the charecter.
now do brute force that using them.


#level-5 :

here the spaces are blocked so in the url give the tab space(%09) instead of the normal space charecter(%20) because the code blocks the normal space but does not check for the tab space or %09 in the url so we can bypass.
query -- ?pw'%09||%09id='admin'--%09
%09 -- the ascii form for the tab space.

#level-6 :

in the level the OR and AND are blocked so as we were using the double pipe(||) does not matter for us instead of using the pipe if we use the or then we need to use the || again.

query -- ?pw' || id='admin'-- 

#level-7 :

this level os combination of lvl 6 and lvl 4 give the ascii charecter of and as that is blocked and then procced with the lvl 4 process giving it to the burp suite and brute force that.

and - && - %26%26(ascii)

#level-8 :

this level the id is the parameter and it requires admin as the id.that is blocked using the preg_match.

the preg match does not look for the casing and also the sql database as well that means if i give the id=Admin that will bypass because the preg_match is case sensitive and the database is insensitive that returns for the value "admin" from the database and in the if condition that satisfies as the output from the database will be "admin".

#level-9 :




