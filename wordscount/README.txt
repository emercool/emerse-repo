Write a Hadoop/Yarn MapReduce application that takes as input 50 Wikipedia web pages dedicated to the US states, found within states.tar.gz, and:

Computes how many times the words “education”, “politics”, “sports”, and “agriculture” appear in each file. Then, the program outputs the number of states for which each of these words is dominant (i.e., appears more times than the other three words).

Identify all states that have the same ranking of these four words. For example, NY, NJ, PA may have the ranking 1. Politics; 2. Sports. 3. Agriculture; 4. Education (meaning “politics” appears more times than “sports” in the Wikipedia file of the state, “sports” appears more times than “agriculture”, etc.)

Part I

Executing the jar file with the input files:

sudo /usr/local/hadoop/bin/hadoop jar wordcount.jar com.code.wordcountPackage.WordCount /data/states /data/firstOuput/


Observe what is in the Output folder:

sudo /usr/local/hadoop/bin/hdfs dfs -ls /data/firstOuput/

Move the output file "part-r-00000" to the home directory:

sudo /usr/local/hadoop/bin/hdfs dfs -mv /data/firstOuput/part-r-00000 /home/emersecool/

Change the permission of the output file and view its contents:

sudo chmod 777 part-r-00000 

cat part-r-00000

file:/data/states/Alabama	education
file:/data/states/Alaska	politics
file:/data/states/Arizona	education
file:/data/states/Arkansas	education
file:/data/states/California	education
file:/data/states/Colorado	sports
file:/data/states/Connecticut	sports
file:/data/states/Delaware	education
file:/data/states/Florida	education
file:/data/states/Georgia	politics
file:/data/states/Hawaii	education
file:/data/states/Idaho	politics
file:/data/states/Illinois	sports
file:/data/states/Indiana	sports
file:/data/states/Iowa	education
file:/data/states/Kansas	education
file:/data/states/Kentucky	education
file:/data/states/Louisiana	education
file:/data/states/Maine	politics
file:/data/states/Maryland	education
file:/data/states/Massachusetts	politics
file:/data/states/Michigan	education
file:/data/states/Minnesota	sports
file:/data/states/Mississippi	education
file:/data/states/Missouri	education
file:/data/states/Montana	sports
file:/data/states/Nebraska	sports
file:/data/states/Nevada	politics
file:/data/states/New_Hampshire	politics
file:/data/states/New_Jersey	sports
file:/data/states/New_Mexico	education
file:/data/states/New_York	education
file:/data/states/North_Carolina	education
file:/data/states/North_Dakota	politics
file:/data/states/Ohio	education
file:/data/states/Oklahoma	education
file:/data/states/Oregon	education
file:/data/states/Pennsylvania	education
file:/data/states/Rhode_Island	politics
file:/data/states/South_Carolina	education
file:/data/states/South_Dakota	sports
file:/data/states/Tennessee	education
file:/data/states/Texas	education
file:/data/states/Utah	politics
file:/data/states/Vermont	education
file:/data/states/Virginia	education
file:/data/states/Washington	education
file:/data/states/West_Virginia	education
file:/data/states/Wisconsin	politics
file:/data/states/Wyoming	education

Remove the first column of the file and redirect it to a new file for just a list of different category:

cut -f2 part-r-00000 &> wordcount1.txt

Move the new input file of states list to the input folder:

sudo mv wordcount1.txt /home/emersecool/data/

Run the jar file to find the count of the different category:

sudo /usr/local/hadoop/bin/hadoop jar finalwordcount.jar com.code.finalwordcount.FinalWordCount ~/data/wordcount1.txt /data/finalWordCount1/

View the final output file of word count:

sudo /usr/local/hadoop/bin/hdfs dfs -cat /data/finalWordCount1/part-r-00000 

education	30
politics	11
sports	9


Part II

Run the jar file to find Word Count Ranking:

sudo /usr/local/hadoop/bin/hadoop jar wordcountranking.jar wordcountrank.WordCountRanking /data/states/ /data/wordcountRankingFinal/

Viewing the output File:

sudo /usr/local/hadoop/bin/hdfs dfs -cat /data/wordcountRankingFinal/part-r-00000 


education;agriculture;politics;sports	Mississippi, Iowa
education;agriculture;sports;politics	Pennsylvania
education;politics;agriculture;sports	Tennessee
education;politics;sports;agriculture	Alabama, West_Virginia, Virginia, Vermont, Texas, South_Carolina, Oregon, Ohio, North_Carolina, New_York, Wyoming, Michigan, Kentucky, Hawaii, Delaware, California, Arkansas
education;sports;agriculture;politics	Oklahoma
education;sports;politics;agriculture	Louisiana, Kansas, Arizona, Florida, Washington, Missouri, Maryland, New_Mexico
politics;agriculture;education;sports	North_Dakota
politics;education;agriculture;sports	Alaska
politics;education;sports;agriculture	Idaho, Nevada, Maine, New_Hampshire, Massachusetts
politics;sports;agriculture;education	Wisconsin
politics;sports;education	Rhode_Island
politics;sports;education;agriculture	Utah, Georgia
sports;education;politics;agriculture	South_Dakota, Illinois, Indiana, Connecticut, Montana, New_Jersey
sports;politics;education;agriculture	Colorado, Minnesota, Nebraska















