
so i decided to do the github recon on this api.example.com

i was started with “api.example.com” search, i got 30k results ,but we already know only possible to see 5 pages only. so we neeed filter out the details, i already read the api documents ,so i add “x-auth-token”.

final dork was {“api.example.com” x-auth-token }

i got 10 k results ,then i start looking for x-auth-token. more tokens i got .every token shows invalid.so i observed one thing here in results every code repositroy shows “x-auth-token :” and some results shows “x-auth-token” only. so just modified the dork .just add :

“api.example.com” x-auth-token:

i got nearly 3k results ,again i start checking every token, finally i got one token and i got this token in company repository example section.and also it has access token and store id .without store id we cant exploit.

then finally exploit the token ,its allowed to add or delete or modify the products.



