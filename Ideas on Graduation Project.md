1. [[Recommendation Systems]] 
	the app can start as knowledge-base recommendation system then
	content-based one focusing on both the client(buyer of the service)
	and freelancer(skilled worker/developer) features.
	metadata + an interaction matrix you can use a neural networks to create 
		a hybrid content-based, collaborative filtering, and knowledge-based recommendations system.
	The app will have two recommendation Systems:
	
	a. Freelancers/Tasks recommender: Shows open tasks to freelancers, the task should be relevant , 
		1. Freelancers Features:
			1. category
			2. address / city : irrelevant in case of developer
			3. rating: **TODO**-> find how to calculate rating. ([weighted average - algorithm used to calculate 5 star ratings - Stack Overflow](https://stackoverflow.com/questions/10196579/algorithm-used-to-calculate-5-star-ratings))
		2. Tasks Features:
			1. category
			2. location : irrelevant in case of developer
			3. status
			4. Description -> tags: task description should be generated to tags (**classification problem**), try to get data from Arabic like خمسات/مستقل (**Web scrapping**)
		Plan:
			1. Decide what features to use from database and what to make . ([weighted average - algorithm used to calculate 5 star ratings - Stack Overflow](https://stackoverflow.com/questions/10196579/algorithm-used-to-calculate-5-star-ratings))
			2. web scrapping from مستقل to have tags and description
			3. build a tag classification system.
			4. make a dataset (a .csv file) using Excel. 
			5. Decide on a recommendation system type
			6. Build a recommendation system
			7. Evaluation metrics ([Evaluation Metrics for Recommender Systems | by Claire Longo | Towards Data Science](https://towardsdatascience.com/evaluation-metrics-for-recommender-systems-df56c6611093))
			8. Deployment
	search :
	- light FM model
	- FAISS (Facebook AI Similarity Search)
	- Mahout-recommender
	b. Client/Freelancers recommender : shows freelancers to client based on the open tasks, (shows top rated freelancers in each category in the beginning )
		1. Freelancers Features:
		2. Client Features / Task Features?:
		
1. [[Chatbot]]
	1. Source :([Mastering Chatbots with Botpress, Rasa3, RAG & LLMs Flowise | Udemy](https://www.udemy.com/course/mastering-chatbots-using-botpress-rasa-and-transformers/?couponCode=24T3FS41524))