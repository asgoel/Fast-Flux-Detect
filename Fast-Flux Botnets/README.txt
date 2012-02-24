fluxDetect - A Heuristic Approach to Detecting Fast-Flux Botnets

Created by Ashutosh Goel, MITRE Corporation, G024-National Intelligence Security, Summer 2011 Intern



------------------------INSTALLATION (Required Libraries)--------------------------------------------


	fluxDetect is a python program that MUST be run on a Linux based system AS ROOT, due to the fact that it uses certain bash scripts. Other required libraries (see
 	dependences folder) include:

	1. pycap (and other required dependencies - see http://pycap.sourceforge.net/ for more information)

	2. jpype (see http://jpype.sourceforge.net/). Furthermore, the JPypeObjectInputStream.class file MUST be added to the build path

	3. weka (the jar file must be added to the build path). NOTE: PLEASE use the jar file included with this distribution when running weka. Otherwise, the models will not
 
		 load. If a different build/version of weka is used to create models, please add THAT jar file to your build path.

	Also, the system will run better if connected to a public DNS, such as Google Public DNS, as opposed to the MITRE proxy.



------------------------TRAINING A CLASSIFIER-----------------------------------------------------------



	1. To train the classifier, enter a set of good and bad URLs into the files "benign.txt" and
   "malicious.txt" respectively
	
2. Run the program
 FFDetect.py (IT IS EXECUTABLE)
	3. If you want to read the locations, timezones, and delays from previous written files, type 'y', else type 'n' or press enter
	
4. The results will be outputted into the file "data.txt"
	
5. Copy the results from "data.txt" into the data section of the file "numerictraining.arff"
	
6. Open the Weka Explorer and open the "numerictraining.arff" file
	
7. Go to the Classifier tab, choose the algorithm of your choice (the AdaBoostM1 is located under meta)
	(For the AdaBoostM1, 30 iterations of the "weak learner" were used)
	
8. Run the classifier and save the model 



------------------------TESTING A CLASSIFIER WITH PRE-LABELED URLs--------------------------------------

	

1. Enter the desired good URLs into the file "testbenign.txt" and the desired bad URLs into the file "testmalicious.txt"
	
2. Run the program FFDetect.py (IT IS EXECUTABLE): it will prompt to read from files, as with training
	
3. The program will output the results into the "data.txt"
	
4. Copy the results from "data.txt" into the data section of the file "numerictesting.arff"
	
5. Open the WekaExplorer, and open the "numerictraining.arff" file
	
6. Go to the Classifier tab, right-click on the Result list, and Load the appropriate model
	
7. Under Test options, set the supplied test set to "numerictesting.arff"
	
8. Right click on the model, and select "Re-evaluate model on current test set"



-----------------------TESTING A CLASSIFIER ON UNLABELED URLs-------------------------------------------
	
	

1. Uncomment the appropriate section in the program (be sure to comment out the train/test section)
	
2. Enter the desired URLs into "test.txt"
	
3. Run the program FFDetect.py (IT IS EXECUTABLE), being sure to input the exact name of the model as it was saved (ex. "MODEL_NAME.model"), when prompted
	
4. The program will print out the result of the classification for each URL in the file "testresults.txt"

		0.0 indicates fastflux, 1.0 indicates benign
	


-----------------------------------------------------------------------------------------------------------

DESCRIPTION OF FILES CONTAINED WITHIN THE FOLDER:

	A_locations.txt - The list of the latitude/longitude coordinates for each IP address in the A records of each domain used for training
	A_lookups.txt - The list of the IP addresses associated with the A records for each domain used for training
	A_timezones.txt - The list of timezones for each IP address in the A records of each domain used for training
	benign.txt - List of good URLs used for training
	document_fetch_delays_benign.txt - The average and standard deviation of the document fetch delay for each benign URL 
	document_fetch_delays_fastflux.txt - The average and standard deviation of the document fetch delay for each fastflux URL
	effective_tld_names.dat.txt - A list of all currently used Top Level Domains (tlds)
	FFDetect.py - Program
	fluxDetect.docx - Documentation
	ipgeo.txt - temporary output file used by program when doing geolocation of IP addresses
	malicious.txt - List of fastflux URLs used for training
	network_delays_benign.txt - The average and standard deviation of the network delays for each benign URL
	network_delays_fastflux.txt - The average and standard deviation of the network delays for each fastflux URL
	NS_locations.txt - The list of the latitude/longitude coordinates for each IP address in the NS records of each domain used for training
	NS_lookups.txt - The list of the IP addresses associated with the NS records for each domain used in training
	NS_timezones.txt - The list of timezones for each IP address in the NS records of each domain used for training
	numerictesting.arff - weka data file used when classifying pre-labeled test urls
	numerictraining.arff - weka data file used when building a classifier using training data
	output.txt - temporary output file used by program when doing dig lookups of domains
	processing_delays_benign.txt - The average and standard deviation of the processing delays for each benign URL
	processing_delays_fastflux.txt - The average and standard deviation of the processing delays for each fastflux URL
	test.txt - List of unlabeled URLs used for testing
	testbenign.txt - List of pre-labeled benign URLs used for testing
	testmalicious.txt - List of pre-labeled fastflux URLs used for testing
	testresults.txt - The output file of the un-labeled URL testing
	whoisoutput.txt - Temporary file used by program when doing whois lookups