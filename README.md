# Election_Analysis

## Overview of Election Audit
The election commission has requested additional data for an elecction audit.

  *  The voter turnout for each county
  *  The percentage of votes from each county out of the total count
  *  The county with the highest turnout

This audit will include the new results with an overview of methods use to aggregate the data.  Finally
an analysis will be provided to give uses of the data.

## Election-Audit Results

The following list will provide specific election outcomes with examples of the code used to develop the outcomes
as support.

  * Number of votes cast in the congressional election
    The total number of votes cast in the congressional election were 369,711.
    ![total votes](https://user-images.githubusercontent.com/100876517/162644290-bd33feab-edf6-479e-8bb7-a4f584635778.png)
    
    The section of the code to provide the total votes is highlighted below
    
   '''
   
    #For each row in the CSV file.
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
        
    #Save the results to our text file.
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
 
  
  * Breakdown of the number of votes and the percentage of total votes for each county in the precinct
  
    The breakdown of votes by county is as follows:
    
    ![county votes](https://user-images.githubusercontent.com/100876517/162644299-6375faf7-d679-4509-b588-95bc15679854.png)
    
    **Example Code**
    
    '''
    
        #6a: Write a for loop to get the county from the county dictionary.
        for county_name in county_votes:

        #6b: Retrieve the county vote count.
        
        votes_county = county_votes.get(county_name)

        #6c: Calculate the percentage of votes for the county.
        
        county_percentage = float(votes_county) / float(total_votes) * 100
        county_results = (
            f"{county_name}: {county_percentage:.1f}% ({votes_county:,})\n")

         #6d: Print the county results to the terminal.
         
        print(county_results)

         #6e: Save the county votes to a text file.
         
        txt_file.write(county_results)

         #6f: Write an if statement to determine the winning county and get its vote count.
         
        if (votes_county > winning_county_vote) and (county_percentage > winning_county_percentage):
            winning_county_vote = votes_county
            winning_county_name = county_name
            winning_county_percentage = county_percentage

    '''
         
  * County with largest number of votes
    The county with the largest number of votes was Denver County.  Denver had 306,055 votes or 82.8% of the total.
    
      
    ![denver](https://user-images.githubusercontent.com/100876517/162644303-a570ab6b-c627-40f3-9070-e27a075bb0c1.png)
    
    ***Example Code***
    
    
 '''
   
       
     #7: Print the county with the largest turnout to the terminal.
     
    winning_county_summary = (
    
        f"-------------------------\n"
        
        f"Largest County Turnout: {winning_county_name}\n"
        
        f"-------------------------\n")
        
    print(winning_county_summary)

    #8: Save the county with the largest turnout to a text file.
    
    txt_file.write(winning_county_summary)
    
  '''  
      
  * Breakdown of the number of votes and the percentage of the total votes each candidate received
  
    ![candidate votes](https://user-images.githubusercontent.com/100876517/162644308-144c341d-571e-4333-b789-896c02328181.png)
    
    ***Example Code***
    
      '''
      
      
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
     
     
     
     
        '''
    
    
         
  * Election winner with vote count and percentage of total votes
  
    ![winner](https://user-images.githubusercontent.com/100876517/162644310-dcf3f169-22f2-49be-abcb-995da01ae276.png)
    
    ***Example Code***
    
   '''
    
        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

       #Print the winning candidate (to terminal)
    
    
      winning_candidate_summary = (
    
          f"-------------------------\n"
          f"Winner: {winning_candidate}\n"
          f"Winning Vote Count: {winning_count:,}\n"
          f"Winning Percentage: {winning_percentage:.1f}%\n"
          f"-------------------------\n")
      print(winning_candidate_summary)

      #Save the winning candidate's name to the text file
      txt_file.write(winning_candidate_summary)
    
    
    '''


 
### Election-Audit Summary

The code used for this specific election-audit can be modified and used in any election.  The code can be modified to include additional voter data or to combine the county and candidate data to show trends for candidate vote by county. 
