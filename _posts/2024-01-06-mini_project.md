## mini project
### sensitive data scraping project
- store domains in a csv file
- run the software
- sofware finds the subdomains by subdmain enumeraion
- for each subdomain using katana it crawls all pages
- for each page we save bas64 encoded data and extract the sensitive info like emails,phone no
- store the whole result in a json
### Automated Android App analysis at high scale
- mobsf is used to perform static and dynaic analysis
- only one vulnerable apk can be tested at once that too with user interactive interaction
- by this software user is given the choice to select multiple apk via file upload userinterface
- all apks will be anaylzed and result will be stored for each apk in a separate json file

### misc
- added authentication feature to mobsf
- by this the port mobsf is running can only be accessed with our process
- wrote a python api wrapper for mobsf i.e interact with mobsf using python cli
