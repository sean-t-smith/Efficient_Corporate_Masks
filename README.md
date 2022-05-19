# Efficient_Corporate_Masks

## Goal
To improve the efficiency of password cracking using hashcat mask attacks.

## History
Forked from the work of golem445 who compiled a list of 8-14 character Hashcat masks based on an analysis of 1.5 million NTLM hashes cracked during pentesting. I started using these lists, but quickly realized that it was taking a long time with my limited GPU cracking resources... I needed to re-order and efficiently prioritize the masks somehow.  Luckily, golem445 included the "corp_8-14.statsgen" file which included the frequency that each mask in the data set was found.  The frequency along with the mask gave me everything that I needed to prioritize the list.

## Methodology
1) Imported the "corp_8-14.statsgen" file into the MS Excel file: hcmask_Generator_9000.xlsx
2) Separated the mask and occurrence into different columns.
2) Created a column that counted the total characters represented by each mask.
3) Created a column that calculated the total keyspace of each mask.
4) Created a column that assigned an efficiency score to each mask using the formula: (occurrence / keyspace) * 1 Trillion
5) Sorted the entire spreadsheet by the efficiency score
6) Filtered the spreadsheet by characters and exported the sorted masks into new "Efficient" .hcmask files.

## Usage

In your process for cracking passwords, these files can be used as a last step.  My recommended password cracking attack order is below:

1) Basic dictionary attack... ie RockYou
2) Brute force all permutations 1-7 character length passwords... this does not take long given the minimal keyspace of this group.
3) Targeted dictionary attack... create a custom lowercase word list using CeWL, local sports teams, city names, mascots, etc and apply the best64.rule
4) Analyze the set of cracked passwords for potential patterns, run targeted attacks which reflect those patterns.
5) BIG dictionary attack... run the passwords through the largest wordlist you have.
6) Analyze any newly cracked passwords for potential patterns, run targeted attacks which reflect those patterns.
7) Use this repository of work and run the "Efficient_#.hcmask" from this repo according to your needs.
