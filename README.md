# pf2e-cardforge

**pf2e-cardforge** is a set of scripts and templates for generating PF2e reference cards using [Nandeck](https://www.nandeck.com) and Google Sheets. The reference cards are designed to streamline prep and gameplay with layouts that are quick to parse and can be created for spells, feats, items, and more.

|       |       |       |
| ----- | ----- | ----- |
| <img src="assets/card_examples/Demoralize_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Feint_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Trip_front.png" style="width:300; height:auto;"> |
| <img src="assets/card_examples/Alchemist&apos;s_Fire_(Lesser)_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Alcohol_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Heal_front.png" style="width:300; height:auto;"> |
| <img src="assets/card_examples/Elemental_Blast_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Intimidating_Strike_front.png" style="width:300; height:auto;"> | <img src="assets/card_examples/Vitality_Lash_front.png" style="width:300; height:auto;"> |


## Installation/Setup

1. **Clone/download this Repo**

2. **Download the Fonts**  
   Two special fonts are used for the cards. Both fonts match the official Pathfinder fonts fairly well, which is why they've been selected. However, these are not installed on most machines by default, so you will need to download them and install them on your computer. 
   
   Below are links to where I have found the fonts myself. If one of them don't work/no longer exists/whatever, you might have to find the font somewhere else. Alternatively, you can use different fonts by editing the scripts (more on this later).
   - [CrimsonPro-Variable.ttf](https://www.fontshare.com/fonts/crimson-pro). Click "Download Family", then open the .zip file and go into `CrimsonPro_Complete -> Fonts -> TTF` to find the file.
   - [Taroca Regular.ttf](https://freefonts.co/fonts/taroca-regular). Click "Download font", then open the .zip file and go into `Taroca Regular` to find the file.

   Once you have the .ttf file, double-click it to open it, then click the "Install" button. I also save them into the "Font" folder just in case I need them again later, but that is not a necessary step.

3. **Download Nandeck**  
   Download from [https://www.nandeck.com](https://www.nandeck.com). NOTE: As of writing this, the latest version `1.28.2` contains a bug that means text doesn't scale properly, causing cards to have a lot of empty space. It is confirmed that version `1.28.3.beta3` contains a fix for this issue, but you will need to go to the Discord to find a link to that version.

   In order to verify that you have a version that fixes the issue, launch Nandeck and click "Open deck", then open the `Test_DynamicBoxLayout.txt` file. Click "Validate deck" and then "Build deck". If the result is similar to the first image below, all is good. If it is similar to the second image, you need to find a different version.

   |       |       |
   | ----- | ----- |
   | <img src="assets/verify_nandeck_version/proper_result.png" style="width:300; height:auto;"> | <img src="assets/verify_nandeck_version/incorrect_result.png" style="width:300; height:auto;"> |
   

4. **Copy the Google Sheets Template**  
   Create a copy of the [Nandeck PF2e Card Data](https://docs.google.com/spreadsheets/d/1eklVjtuwi2jCBNKpKFjLM-377riymgW4eLRoURrabAw/copy) Google Sheet. This sheet designed to work with the scripts and allow for easy entry of data for new cards.
   1. In the new copy, Click the "Share" button and set it so "Anyone with the link" has "Viewer" access. This allows Nandeck to access the sheet. Then click the "Copy link" button
   2. Paste the link somewhere (Notepad or similar) and remove `https://docs.google.com/spreadsheets/d/` and everything after the final `/`. It should leave you with a long string similar to `1aBcD3fGhI_JkLmNoPqRsTuVwXyZT9876543210ab` which is the ID of the Google Sheet.
   3. Open the `PF2e Generate Cards For Sheet.txt` file and replace `GOOGLE_SHEETS_ID_GOES_HERE` with the ID you just found. Save the file.

Everything should now be ready for you to start creating cards.




## Usage Instructions

Creating a new card and readying it for print is a 3-step process: You need to add the card data to the google sheet, then create the card images using the provided scripts, and finally create a PDF from the card images. Each step is explained below.

Note: The first time you validate the scripts, you might be asked to enabled IE11. Accept, as otherwise the script won't work.


### Add Card Data to Google Sheet

The Google Sheet you have created a copy of comes with a lot of examples already, which should help you figure out what to do. You can do whatever you want with the examples, but if you want to keep them for reference without creating cards for them, simply make sure the "Enable" column isn't ticked. There is also a README sheet, which explains the basics of the sheet.

That said, here are some instructions on how to fill in a new card:

1. Figure out what you want to create a card for and figure out which sheet the feature/spell/item belongs to:
    - "Skill_vs_Defense" is for any action/feature where a character rolls a check against a target's defense (fx. _Trip_, _Demoralize_, etc.). This doesn't include spells.
    - "Spells" is for spells.
    - "Simple_Action" is for any action/feature that does not specifically include a check against a defense. This is most class features or feats.
    - "Item_Consumables" is for consumable items.
    - "Custom_Cards" is for other custom ideas.

2. Go to the sheet and start filling in the information you want on the card. Dark green columns are mandatory while light green columns are optional. For example for _Demoralize_, the "Requirement" column will not be filled in, as _Demoralize_ has no requirements.

    The sheets are set up to allow for easy data inputting, and will handle the formatting that is common across all cards of the same type. For example, filling data into a row in "Simple_Action" will handle formatting the degrees of success correctly.

You can add more custom formatting in the different columns such as making text **bold**, _italic_, etc. The instructions are included in the README sheet.


### Create Card Images

1. Launch Nandeck, click "Open deck", and then select the `PF2e Generate Cards For Sheet.txt` file. Nandeck will remember which "decks" you have opened, so this step should not be necessary in the future.
2. Verify that the `LINK = JOIN(` command references your copy of the "Nandeck PF2e Card Data" Google Sheets, which you created in step 4 of Installation.
3. Set `[card_category]` to the sheet tab you want to create cards from.
4. Click the "Validate deck" button. If the terminal below does not say "Deck valid", you will have to figure out what the error is and fix it. Otherwise all is good and you can click "Build deck".
5. The script will now start creating all the cards that have been flagged as "Enable" in the Google Sheet. They will be saved in the `Cards/` directory. It might look like Nandeck is attempting to create around 200 cards, that is because even empty rows are considered a card due to the formatting forumlas that have been used in the sheets. Just ignore that. Nandeck will make only create the Enabled cards.
    
   Note that each card may take a while to create, as there's a lot of calculations of text size going on in the background. On my machine, it is around 6 seconds per card.

Using the script as is, only images for the front side of the cards will be created. There are commands at the bottom of the script that cna be enabled to also create the backs of the cards, which you can enable if you want.


### Create PDFs

1. In Nandeck, open the `PF2e Create PDF.txt` file.
2. Set `[card_category]` to folder you want to pull the images from (the same name as the sheet in Google Sheets).
3. Set `[file_name_suffix]` to whatever you want. This value is added to the end of the PDF name. It can be changed between runs to avoid overwriting existing PDF files.
4. Determine if you want the PDF to be created as duplex (printing on front and back of the paper) or not. This is only relevant if you have created both fronts and backs of cards. If yes, enable line 83-85 and outcomment line 88. If no, leave it as is.
5. Click the "Validate deck". If the terminal below does not say "Deck valid", you will have to figure out what the error is and fix it. Otherwise all is good and you can click "Build deck".

By default, the script will take all images in the given `[card_category]` folder and create a single PDF with all of them. If you only want certain cards (or want cards from multiple different folders), see the examples on line 26 to 50 of the script on how to accomplish that.




## Modifying the Scripts (Optional)

See [MODIFYING_THE_SCRIPTS.md](./MODIFYING_THE_SCRIPTS.md)




## Creating a new Template (Optional)

See [CREATING_A_NEW_TEMPLATE.md](./CREATING_A_NEW_TEMPLATE.md)




## Contributing

If you have improvements for layout, new types of cards, or whatever else, feel free to fork the project and submit a PR.

Please make sure any contributions respect the open-source license and avoid including copyrighted Pathfinder content.




## Licenses

This project is licensed under the [MIT License](LICENSE). You are free to use, modify, and redistribute this code as you like, with attribution.

The action icons have been created by me based on the ones found in the [foundryvtt repo](https://github.com/foundryvtt/pf2e/tree/master/static/icons/actions).
