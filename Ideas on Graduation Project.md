1. [[Recommendation Systems]] 
	the app can start as knowledge-base recommendation system then
	content-based one focusing on both the user(buyer of the service)
	and item(skilled worker) features.
	metadata + an interaction matrix you can use a neural networks to create 
		a hybrid content-based, collaborative filtering, and knowledge-based recommendations system.
	The app will have two recommendation Systems:
	
	a. Freelancers/Tasks recommender: Shows open tasks to freelancers, the task should be relevant , 
		1. Freelancers Features:
			1. category
			2. address / city : irrelevant in case of developer
			3. rating: **TODO**-> find how to calculate rating.
		2. Tasks Features:
			1. category
			2. location : irrelevant in case of developer
			3. status
			4. Description -> tags: task description should be generated to tags (**classification problem**), try to get data from Arabic like خمسات/مستقل (**Web scrapping**)
	
	b. Client/Freelancers recommender : shows freelancers to client based on the open tasks, (shows top rated freelancers in each category in the beginning )
		1. Freelancers Features:
		2. Client Features / Task Features?:
		
1. [[Chatbot]]