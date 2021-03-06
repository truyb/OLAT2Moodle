 _____________
|             |
| OLAT2Moodle |
|_____________|

OLAT2Moodle is a parser written in PHP that
converts OLAT backup ZIP files to Moodle backup MBZ files.

The repository contains a basic upload HTML page, and an output page
that shows if the course got parsed correctly or not (with error handling
showing the faults).


=============MIGRATION============

** USERS WILL NOT BE MIGRATED OVER TO MOODLE, ONLY THE COURSE ITSELF **

Moodle DOES NOT support sub-activities in sub-activities (without modules),
this has been remedied by using indentation (which is purely visual)

- Top level OLAT course elements will become Moodle sections
- Things that will get migrated (with what it will become between parentheses):
  - Empty structures (Label)
  - Stuctures (Page)
  - Pages (Page)
  - Folders (Folder)
    - Including the containing data
  - Tasks (Assignment)
  - Tests (Quiz)
  - Self tests (Quiz)
  - Surveys (Quiz)
  - Files (Resource)
  - Wikis (Wiki)
    - This is just an empty shell of the wiki    
    - Wikis can be migrated manually by exporting the
      wiki activity itself to CP in OLAT, and importing
      it as an IMS package in Moodle. It will not be a
      wiki but the data will at least be available.

===========REQUIREMENTS===========

- Decent hardware. A lot of files will get moved around and this means 
  that quite some memory will be used in the process.
- A webserver (Apache or nginx) 
  with PHP 5.4 or up (PHP 5.5 recommended at time of writing).
  - If running the project off a Linux machine,
    make sure that the de_DE locale is available
    (this is to make sure files with strange characters will unzip correctly).
  - Make sure that the webserver has permission to 
    create, modify and delete files in its own project folder.


===========PHP SETTINGS===========

To make sure the parser runs correctly, 
some values have to be edited in php.ini.

fileinfo
- Make sure that the fileinfo extension is enabled in PHP.

  extension=php_fileinfo.dll

upload_max_filesize
post_max_size
- The value should increase up to the size of 
  the biggest OLAT course that will get imported.

max_execution_time
- The default value is too short for 
  most scripts to complete (for big courses), 
  increase this value to make sure that every script
  has enough time to complete successfully.

  RECOMMENDED VALUE: 120

memory_limit
- This value should be increased because a lot of files get 
  moved around during the process and this might take quite some memory 
  (depending on the size of the course).

  RECOMMENDED VALUE: 512M


==========MOODLE SETTINGS=========

- qtype_multichoiceset module is required
  - Get the version for your Moodle version here:
    https://github.com/jmvedrine/moodle-qtype_multichoiceset


==================================

Initial version made by Bert Truyens and Sam Wouters

Thanks to: Adriane Boyd for qtype_multichoiceset
           Roger Thomas for his recursive ZIP function
     
Date of writing: May 2014
