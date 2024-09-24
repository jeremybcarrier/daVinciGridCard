# daVinciGridCard
Grid card implementation via DaVinci

###This project is not a product provided by PingIdentity and is not supported by PingIdentity.

##What this project provides
This project provides a DaVinci implementation of legacy multifactor grid cards.  It provides a mechanism to generate grid cards and store them against users in PingOne as well as validate a user by asking for values from the grid card.

##Pre-requisites
- A PingOne ecosystem with DaVinci as an added service
- A custom User Attribute in PingOne called gridCard of type JSON

##To Use
- Import the two flows to your DaVinci environment
- Update your variables using the Initialize Variables node at the beginning of each flow
- Use Generate Key to create and store a grid card for a user
- Use Validate Grid Card to test the user's grid card

##Notes
- I'm not a UI person, so WYSIWYG - you'll probably wan't to build a nicer UI for this
- This project is built for standalone use.  It can easily be adapted to use in a PingOne flow or other use cases, but instructions for such are not included.
- In the Generate Key flow, the Initialize Variable node:
  - numAllowedCols is the number of columns that the grid card should have
  - numAllowedRows is the number of rows that the grid card should have
  - numCharsPerCell is the number of characters that each grid card cell should contain
  - userId is the PingOne userId you want to update
- In the Validate Grid Card flow, the Initialize Variables node:
  - numCheck is the number of cells you want the user to provide values from
  - userId is the PingOne user against whose grid card you want to validate
  - numAllowedCols is the number of columns that the grid card has (this should match the value in Generate Key)
  - numAllowedRows is the number of rows that the grid card has (this should match the value in Generate Key)
- These flows will automatically create a set of company variables
  - validValuesInGrid is a string containing all of the characters that are valid for use in a grid card
    - OOTB, the capital letters for 'i' and 'o' are not included so that they are not confused with the numbers 1 and 0
  - validColumns is a string containing all of the valid column names
    - OOTB, these are capital letters A-Z, with the exception of 'i' and 'o'
  - validRows is a string containing all of the valid row names
    - OOTB, these are numbers 0-9
- All row and column names are single character
- For this project, the grid card is stored on the PingOne user as a JSON object
  - In this format, the grid card can be read in plain text, or manipulated, by an administrator
