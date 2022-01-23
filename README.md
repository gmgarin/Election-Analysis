# election-analysis
Module 3 Python Challenge

## Overview of Election Audit
### The purpose of this election audit is to summarized the results and obtain additional important information needed by the Colorado Board of Election. The goal was to write a python code that will be ran to analyze the data gathered during election day. Specifically, the election commision wants to know the voter turnout for each county, the percentage of votes from each county out of the total count, and the county with the highest turnout.

## Election Audit Results
### Using Python script, the data was analyzed and showed the following results:
  - **Total Votes:**
    - 369, 711
  - **County Votes**
      - Jefferson: 38,855 (10.5%)
      - Denver: 306,055 (82.8%)
      - Arapahoe: 24,801 (6.7%)
  - **The county with the largest voter turnout is Denver.**
  - **Candidate Votes:**
      - Charles Casper Stockham: 85,213 (23.0%)
      - Diana DeGette: 272,892 (73.8%)
      - Raymon Anthony Doane: 11,606 (3.1%)
  - **Winning Candidate:**
      - Diana DeGette
           - with 272,892 total votes
           - 73.8% of total votes
  
<img width="270" alt="election_analysis" src="https://user-images.githubusercontent.com/96095956/150682118-0012e56f-bc88-47c4-b5a5-e01cd289a181.PNG">

*Election data summary generated on a .txt file*

Python Script used to analyze election data:
    
    ##### 1: Create a county list and county votes dictionary.
            county_list= []
            county_votes = {}

    ##### Track the winning candidate, vote count and percentage
    winning_candidate = ""
    winning_count = 0
    winning_percentage = 0

    #####2: Track the largest county and county voter turnout.
    largest_county_turnout = ""
    largest_county_vote = 0

    #####Read the csv and convert it into a list of dictionaries
    with open(file_to_load) as election_data:
        reader = csv.reader(election_data)

      #####Read the header
        header = next(reader)

       #####For each row in the CSV file.
        for row in reader:

            # Add to the total vote count
            total_votes = total_votes + 1

            # Get the candidate name from each row.
            candidate_name = row[2]

            # 3: Extract the county name from each row.
            county_name = row[1]

            # If the candidate does not match any existing candidate add it to
            # the candidate list
            if candidate_name not in candidate_options:

                # Add the candidate name to the candidate list.
                candidate_options.append(candidate_name)

                # And begin tracking that candidate's voter count.
                candidate_votes[candidate_name] = 0

            # Add a vote to that candidate's count
            candidate_votes[candidate_name] += 1

            # 4a: Write an if statement that checks that the
            # county does not match any existing county in the county list.
            if county_name not in county_list:

                # 4b: Add the existing county to the list of counties.
                county_list.append(county_name)

                # 4c: Begin tracking the county's vote count.
                county_votes[county_name] = 0

            # 5: Add a vote to that county's vote count.
            county_votes[county_name] += 1

    ##### Save the results to our text file.
    with open(file_to_save, "w") as txt_file:

        # Print the final vote count (to terminal)
        election_results = (
            f"\nElection Results\n"
            f"-------------------------\n"
            f"Total Votes: {total_votes:,}\n"
            f"-------------------------\n\n"
            f"County Votes:\n")
        print(election_results, end="")

        txt_file.write(election_results)

        # 6a: Write a for loop to get the county from the county dictionary.
        for county_name in county_votes: 
            # 6b: Retrieve the county vote count.
            county_vote_count = county_votes[county_name]
            # 6c: Calculate the percentage of votes for the county.
            county_vote_percentage = float(county_vote_count)/float(total_votes)*100
            county_results=(
                f"{county_name}: {county_vote_percentage:.1f}% ({county_vote_count:,})\n")
             # 6d: Print the county results to the terminal.
            print(county_results)
             # 6e: Save the county votes to a text file.
            txt_file.write(county_results)
             # 6f: Write an if statement to determine the winning county and get its vote count.
            if (county_vote_count > largest_county_vote):
                largest_county_vote = county_vote_count
                largest_county_turnout = county_name

        # 7: Print the county with the largest turnout to the terminal.
        largest_county_turnout = (
            f"\n-------------------------\n"
            f"Largest County Turnout: {largest_county_turnout}\n"
            f"-------------------------\n")
        print(largest_county_turnout)

        # 8: Save the county with the largest turnout to a text file.
        txt_file.write(largest_county_turnout)
        # Save the final candidate vote count to the text file.
        for candidate_name in candidate_votes:

            # Retrieve vote count and percentage
            votes = candidate_votes.get(candidate_name)
            vote_percentage = float(votes) / float(total_votes) * 100
            candidate_results = (
                f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

            # Print each candidate's voter count and percentage to the
            # terminal.
            print(candidate_results)
            #  Save the candidate results to our text file.
            txt_file.write(candidate_results)

            # Determine winning vote count, winning percentage, and candidate.
            if (votes > winning_count) and (vote_percentage > winning_percentage):
                winning_count = votes
                winning_candidate = candidate_name
                winning_percentage = vote_percentage

        # Print the winning candidate (to terminal)
        winning_candidate_summary = (
            f"-------------------------\n"
            f"Winner: {winning_candidate}\n"
            f"Winning Vote Count: {winning_count:,}\n"
            f"Winning Percentage: {winning_percentage:.1f}%\n"
            f"-------------------------\n")
        print(winning_candidate_summary)

        # Save the winning candidate's name to the text file
        txt_file.write(winning_candidate_summary)


## Election-Audit Summary
### In conclusion, running a Python script is an efficient and effective way of analyzing vast amount of data gathered during election season. It can be modified in many different ways depending on the needed information and available data. For example, in future elections, Python script can also be modified to identify the breakdwon of the numbers of how people voted (i.e. mail, early voting, and election day voting). It can also used to detect potential irregularities like duplicate votes etc.   
        
