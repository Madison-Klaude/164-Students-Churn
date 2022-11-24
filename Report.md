# 164-Students-Churn
I Analyzed 17 Metrics of 164 Students Applying Schools Overseas and Found the Secret of Preventing Customer Churn in Education Services

**Abstract**

When it comes to completing the annual budget for education services, it is often the clients who are uncertain whether to continue the services that managers worry about the most. Unfortunately, the number of students seeking a deferral or refund has been increasing at an alarming rate and will continue to increase in the foreseeable future, posing an unprecedented challenge for education service leaders in China. In this project, I performed an analysis on 17 metrics of 164 students who had applied for schools overseas and had deferred or received refunds of the service we provided them in 2020, so that leaders in this field will be able to provide more satisfactory services to clients, prevent customer churn, boost business performance, and continue to develop their services in a sustainable way. 

**Introduction**

When it comes to completing the annual budget in the education services industry, compared with clients with services already completed, it is often the clients that are in service and are uncertain to continue the services, i.e., those that might want to defer their service contract for one year due to insufficient GRE or TOEFL scores, or want a refund due to a change in overseas study plans, that managers worry about the most. Unfortunately, the number of students seeking a deferral or refund at my then employer increased at an alarming rate in 2020 and 2021 due to a variety of factors, including tense international relations (particularly decoupling between the United States and China), COVID-19, China's double reduction policy, and a growing number of competitors in education services with smaller business scales and more personalised services (I elaborated on these reasons in my previous article, "Four Crises and Prospects of International Education in China", feel free to check it out). Such conditions were seen again in 2022 and will continue to be seen in the foreseeable future, posing an unprecedented challenge for education service leaders in China. If they can provide satisfactory services to these students, they will be able to complete their annual budget and continue to develop their services in a sustainable way. 

With the goal of providing more satisfactory services to students, helping them achieve ideal application results, and boosting our business performance, I decided to perform an analysis on the features of students who had already deferred or received refunds in the previous year (2020), so that we could have a better idea of what we can do for students who are about to ask for a defer or refund this year (2021). Since these students already signed service contracts, keeping them requires far fewer communication costs than convincing potential students who haven't signed contracts to sign as new clients; therefore, spending equal time on keeping them rather than exploring new markets would be an efficient strategy. Since COVID-19 is still having an effect on many customer service industries, especially in China, the results of this study's research on customers who ask for deferred service or refunds will also be helpful and inspiring for business leaders all over the world who have to deal with similar unexpected situations.

**Step 1: Data Collection - 164 Students, 17 Metrics**

The research was done in 2021, so I collected student data from the previous year, which was 2020. The information was obtained from the department's internal weekly report containing student information. A total of 164 students were deferred or received refunds in 2020. Dimensions of students’ data in the original report include:

1.	Students' names
2.	Names of consultants who signed contracts
3.	Names of consultants who provided application services
4.	Service contract types (Half-DIY, Regular, Lead, Elite, and Deluxe)
5.	Service contract prices (which range from 28,000 RMB to 98,000 RMB depending on the type)
6.	Names of students’ undergraduate institutions
7.	Names of students’ graduate institutions (if applicable)
8.	Majors pursued by students at undergraduate institutions
9.	Majors pursued by students at graduate institutions (if applicable)
10.	Majors that students are applying for studying overseas
11.	Students’ undergraduate GPA
12.	Students’ graduate GPA (if applicable)
13.	Students’ GRE scores (if applicable)
14.	Students’ TOEFL scores (if applicable)
15.	Students’ IELTS scores (if applicable)
16.	Students’ GMAT scores (if applicable)
17.	Reasons for their deferral or refund.

In the next part, I will elaborate on data collection, exploratory data analysis, and detailed data analysis.

**Step 2: Data Cleaning - Converting Scales and Types of Data, Importing Data in Google Colab**

In the previous part, I obtained data on 164 students and put them in a .xls file. However, they are not immediately ready for analysis due to different scales or different data types. The following three dimensions were converted:

1.	GPA: Most GPAs used a 4.0 scale, but nine of them used a 100 scale. Using the GPA conversion chart offered by UC Berkeley (https://ieor.berkeley.edu/wp-content/uploads/2019/10/GPA_Conversion_Chart2.pdf), I converted them to a 4.0 scale for further analysis.

2.	GMAT/GRE: Most students had GRE scores, but one student only had GMAT scores. I used the official conversion chart offered by ETS (https://www.ets.org/gre/institutions/admissions/interpretation_resources/mba_comparison_tool?WT.ac=40361_owt06_180820) to convert the GMAT scores to GRE scores. Although the official tool had become unavailable when I wrote the article, there are many alternatives, such as the conversion offered by Manhattan Review (https://www.manhattanreview.com/gmat-to-gre-score-conversion/).

3.	Majors that students pursue, majors that they are applying for, and reasons for their deferral or refund: These three types of data are categorical. I applied one-hot encoding to convert them to discrete data (yes=1, no=0) to identify quantitative findings more effectively. Specific conversions are as follows:

Undergraduate Major (UGMajor): 
-UGLiberalSocial
-UGScience
-UGEngineering
-UGBusiness
-UGArts
Graduate Major (GMajor): 
-GLiberalSocial
-GScience
-GEngineering
-GBusiness
-GArts
Reasons for deferral or refund: 
-Defer
-Refund
-LoseContact (student lost contact with service team members and did not reply them anymore)
-DeferGraduation (student postpone graduation for 6 months or a year, often due to illness or a too low GPA)	
-GapToWork (student took a gap year, often doing a full-time job)
-LackGTScore (student failed to provide sufficient GRE/TOEFL score)
-MentalProblem (student were unable to apply for schools due to mental health issues)
-Rejected (student got rejected by all schools they applied for)
-GoAbroad (student decided to go to a country other than the U.S.)
-U.S. (student decided to go to a school in the U.S. not in the service contract)
-ChinaGrad (student decided to pursue further study in China)

Now we have the data ready for exploratory data analysis and further quantitative analysis. Different from my previous project, in which I analysed data with the original data files on my computer, in this project I adopted Google Colab to analyse data so that the results could be shared with the management and checked by them in a more convenient way. After saving the data file in a .csv format, I set up a Google Drive environment and put the .csv file in Google Drive to analyse the data in Google Colab with the following code.

![Step 2-1](https://user-images.githubusercontent.com/118432046/203782053-8eb7dfa1-4036-46a4-b5fd-eb84fa967e3a.JPG)

![Step 2-2](https://user-images.githubusercontent.com/118432046/203782061-23ec3a25-8731-4f5e-acd8-4bbc3a9c3355.JPG)

And now the data is ready to use in Google Colab.

**Step 3: Data Analysis - Understanding Raw Dataset, Visualizing Features and Correlation**

The following codes are used to get a glimpse of the raw dataset. It confirmed that there are 164 students, and data types include float64, int64, and object.

![Step 3-1](https://user-images.githubusercontent.com/118432046/203782126-fb4449d0-2f14-46fa-a6ef-417a73184178.JPG)

The following step is to explore features between different data dimensions. My assumption was that whether students ask for defer/refund or not is related to the price of their service contract, their GPA grade, and their TOEFL and GRE scores, therefore I chose these four dimensions, and the results are as follows.

![Step 3-2](https://user-images.githubusercontent.com/118432046/203782170-37305071-08b1-4a53-9511-55715cacc893.JPG)

![Step 3-3](https://user-images.githubusercontent.com/118432046/203782232-6f082e11-1425-4ff5-809c-76ec3b34f5f9.JPG)

In order to observe possible trends and derive insights more efficiently, I further used the following codes to check feature distribution and made boxplots to visualize the numerical features. 

![Step 3-4](https://user-images.githubusercontent.com/118432046/203782298-e3b80094-5f7f-4141-96a7-a5f9cd6cb73a.JPG)

![image](https://user-images.githubusercontent.com/118432046/203781307-5ca76eda-a634-4413-80e7-26611b413b7d.png)

Categorical features are also essential in order to interpret the results, therefore the following codes are used to understand them.

![Step 3-6](https://user-images.githubusercontent.com/118432046/203782485-da65bcdb-a9fd-4cb8-9eb7-29a28914bb8c.JPG)
  
![image](https://user-images.githubusercontent.com/118432046/203781532-f4a6c51f-1827-471f-8cfa-e3f8475c225c.png)

Last, in order to explore whether there are correlations between these features and, if so, how they are correlated, I wrote the following codes to identify possible correlations, visualised them in a heatmap, and checked the actual values to perform a more accurate analysis.

![Step 3-7](https://user-images.githubusercontent.com/118432046/203782554-15289f36-6d14-41ba-bd33-9bc85017b5dd.JPG)

![image](https://user-images.githubusercontent.com/118432046/203781566-af873fc1-1369-4227-ad52-1f142574d9c7.png)

![image](https://user-images.githubusercontent.com/118432046/203781609-d7fa2dfe-1481-4734-a1c7-b6363a3e6955.png)

Many interpretations and suggestions that can be implemented in daily business operations can be derived from the above data. I’ll elaborate on the plots and implications in the next part.

**Step 4: Findings, Conclusions, and Inspirations for Strategy and Decision-Making**

Upon examining the three plots, the following three trends can be observed, and suggested ways of making strategic moves are raised.
 
1.	The first trend lies in the box plot for numerical features. The plots of GPA grade and deferred or refunded services (the plots on the top left and top right) show that students with GPAs below 2.3 are more likely to ask for a deferral of their services.
 
-Reason: Their goal, like any other student's, is to be admitted to an ideal school. However, their low GPAs make them less competitive. Rather than applying to multiple schools and being rejected by all of them due to low GPAs, most of them prefer deferring service for a year, which gives them plenty of time to improve their GPAs and do a couple of related internships to boost their competitiveness. The reason they are not likely to choose a refund is that without professional help from professional service teams, preparing application materials on their own lowers their chance of achieving their goals, since one of the most common reasons for application rejection is a low GPA.
 
-Importance: This type of student deserves the management’s attention because, once the service is started and performed in a satisfactory way, the students are unlikely to ask for a refund, which means they are rather secure in the annual budget.
 
-Suggestions: For students whose studies are still in progress, their service teams should devise strategies to help them improve their GPAs, such as communicating with them on a weekly basis to understand their most recent study conditions, offering advice on course selection when new semesters begin, and suggesting they do research projects relevant to their interests and the majors to which they intend to apply. For students who have already graduated and are unable to improve their GPAs anymore, if they want to begin their studies as soon as possible and do not have other plans that will impact their timelines (such as finding a full-time job), the service teams should put more effort into assisting them in finding suitable schools and programmes that they can enrol in as soon as possible. Meanwhile, they should also monitor their progress on application and enrollment to ensure efficiency. 

2.	The second trend is also evident in the box plots: the plots of TOEFL and deferred or refunded services (the top middle one and the middle left one) and GRE and deferred or refunded services (the middle one and the middle right one) indicate two vital numbers: 83 (for TOEFL) and 310 (for GRE). Students who achieve these two scores in this group of 164 are more likely to choose deferral over refund.

-Reason: When students choose deferral or refund, they will take into consideration the costs they have already paid, including sunk costs. Internal data from New Oriental, the largest education technology company in China, revealed that in order to get one extra mark in the GRE, Chinese students need to spend on average 20 hours studying the GRE, and this number is 10 hours for the TOEFL. According to A Snapshot of the Individuals Who Took the GRE® General Test (https://www.ets.org/pdfs/gre/snapshot.pdf) and TOEFL iBT® Test and Score Data Summary (https://www.ets.org/content/dam/ets-org/pdfs/toefl/toefl-ibt-test-score-data-summary-2021.pdf) offered by ETS, the average GRE and TOEFL scores for Chinese (the 164 students in this research belong to this category) are, respectively, 317.9 and 87. Students with a GRE of 310 and a TOEFL of 83 might still need to study for 40 hours of TOEFL and 160 hours of GRE if they choose to defer for another year, but if they choose to refund, especially because they decide not to study in the U.S. anymore, the dozens of hours they have spent on studying for these two exams might become a considerable sunk cost.

-Importance: The significance of this type of student is that they need more professional support, which is often what education service providers can offer them. Apart from having school application divisions, big edtech companies often also have language education divisions with experienced TOEFL and GRE teaching teams. Scheduling courses for these students is a win-win situation for the students and the edtech company as a whole. Smaller edtech companies can also support students by contacting reliable agents that offer TOEFL and GRE teaching services to ensure student success.

-Suggestions: For students who haven’t gotten 83 in TOEFL and 310 in GRE, the service team members should make detailed plans and monitor students’ progress to motivate them to achieve these scores. Meanwhile, interdepartmental awareness about how to deliver effective TOEFL and GRE teaching to this type of student should be raised. Providing these services with the students’ high satisfaction rate will help management achieve its annual budget effectively as a natural result.

3.	The heatmap that shows the correlation between price of contracts, students’ GPA grade, and reasons for their refund reveals the third trend. The top 5 smallest values of correlations, which indicate negative correlations, are -0.295721 (LackGTScore and LoseContact), -0.240260 (Price and LoseContact), -0.189371	(LackGTScore and MentalProblem), -0.145563 (LackGTScore and Grade) and -0.135985	(Grade and Price). The top 5 largest values of correlations, which indicate positive correlations, include 0.178589 (MentalProblem and Price), 0.145645 (Price and Rejected), 0.143215 (LoseContact and Refund), 0.129676 (GapToWork and Refund), 0.114695	(Grade and GoAbroad).

-Reason, Importance, and suggestions: One interesting finding from 0.145645 (Price and Rejected) is that signing expensive contracts wouldn’t lower students’ chances of getting rejected by all the schools they applied for, i.e., wouldn’t increase their chance of being admitted. This is against the common sense of many people, including many practitioners who have worked many years in this field. It is difficult to explain to them that more work does not always result in better results.Many edtech companies in the school application field spend a lot of time and effort writing compelling promotional articles and claiming that students received offers that exceeded their expectations after signing the most expensive contract. Both practitioners and customers should be wary of misinformation and complex customer psychology during the school application process.

Being admitted requires students’ own attitudes and behaviors. That is the power they need in order to improve their GPA, GRE/TOEFL, and prepare competitive application materials. How they can be more motivated and take action is something that current human science hasn’t found a satisfactory answer to. Existing solutions include drugs and therapy, but whether they are legal, safe, and accessible is a question. Even if human science one day solves the question, many edtech companies, especially the smaller ones, still lack the resources and funds to implement the possible plan, which I elaborated on in my previous article, Two Challenges of Applying RPA and Data Analytics in the Education Industry in China (https://medium.com/@Yun_in_Information/two-challenges-of-applying-rpa-and-data-analytics-in-the-education-industry-in-china-ffd4a3fa46ae). For some companies that don’t want to solve the question in a hard but ethical way, they might ask, "Why make so many efforts doing quantitative things we don’t understand when we can lure students in with empty promises and micromanage them?" Sadly, this is what many companies are doing in the edtech market in China.

One possible solution I can think of for edtech professionals is to be inspired by psychologists, ask for their help, and develop information systems and databases to collect students’ data and analyse it. This might be the only way if edtech companies want to achieve growth through quality instead of quantity. External power, such as more expensive service contracts and frequent communication from service teams, might not be sufficient to change results from rejection to admission in school applications. Getting lost in promises might have disastrous consequences, such as difficulty in delivering services and completing budgets due to the large number of deferrals or refunds.

Another finding that is worth noticing is that while many companies list the frequency of contact as an indicator to measure service teams’ business performance, it is unclear whether there is a correlation between contact frequency and application results. What type of student is more likely to lose contact with service teams? The negative correlation between LackGTScore and LoseContact indicate the answer is those who already have sufficient GRE/TOEFL scores. However, to some extent, these students should receive satisfactory application results regardless of the frequency of contact. Frequent communication doesn’t lead to high GPAs, high GRE or TOEFL scores, lower defer or refund rates, or better application results. Every management team should ask themselves, "What is our goal, and what is our priority when the goals cannot be achieved at the same time?" They cannot have everything, and putting too much time into work that is not related to priorities will cause waste and low efficiency.

Meanwhile, the data confirmed multiple existing experience-based observations, such as: 
1.	Students who signed a higher-priced service contract are more likely to have low GPA grades (they believe deluxe services can compensate for GPA deficiencies), are more likely to have mental health issues, and are less likely to lose contact (they have higher expectations of mental support).
2.	Students with insufficient TOEFL or GRE scores are more likely to have low GPAs and are less likely to lose contact with their service teams (since they need more professional help).
3.	Students with higher GPAs are more likely to choose other foreign countries other than the U.S. when they ask for a defer/refund.
4.	Among the reasons for refunds, the most related ones are losing contact and taking a gap year to work. 

**Step 5: Revisiting the Question**

Overall, when I return to the question of why students want to defer or refund, I have gotten these fruitful results and reflections.

In a broader sense, the international relationship has been drastically different from a decade or two decades ago, with widespread misinformation, as I discussed in my previous work, Four Crises and Prospects of International Education in China (https://medium.com/@Yun_in_Information/four-crises-and-prospects-of-international-education-in-China-1-73b037f92089). If students see the news that another gunshot happened in the U.S. or that millions of people died from COVID-19 and experience that every year tens of thousands of students return to China from the U.S. upon graduation and compete for jobs that they are overqualified for, they might ask, "Why go to the U.S. when we can enrol in a school with a higher rank with less cost in the UK?" How can a consultant with ethics persuade students that the U.S. is still a popular country and they should definitely go there without listening to their concerns and taking their personal conditions into consideration?

From the perspective of application service providers, they should do more research, especially quantitative ones, to determine what affects students' application results. For example, GPA is much more important than we thought and should be the focus of much of our daily work. Sadly, although there are edtech companies that are performing quantitative research, many of them are inefficient or even unethical. How many of the edtech practitioners are not helping students as they promised when they claimed they were embracing technology? This is a worrying trend that raises a question that is worthy for every practitioner to think about.

Finally, from the standpoint of individual students, whose motivation and actions are difficult to change, this is a question that requires not only practitioners in edtech but also scientists and experienced professionals in business operations to work together to answer, and I sincerely hope we can find the answer in the near future.
