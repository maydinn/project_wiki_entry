# project_wiki_entry

DESCRIPTION:

In this repository, you will find the analyzes of Wikipedias entries by languages and its ratio to population and GDP per capita

DATA:

wiki entry table : https://meta.wikimedia.org/wiki/List_of_Wikipedias

population : https://raw.githubusercontent.com/datasets/population/master/data/population.csv

GDP Per Capita: https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)_per_capita


examples of some important used methods:


#to download data from github for language and countries

url = 'https://raw.githubusercontent.com/annexare/Countries/master/data/countries.json'
count_lang = pd.read_json(url).T


#to check if there is any empty list at languages column

count_lang[count_lang.languages.apply(lambda x: len(x)<1)]


#to get first value from the list at languages column

count_lang['first_language']=count_lang.languages.apply(lambda x: x[0])


#to assign a population of country for each wiki language

wiki=pd.merge(wiki, pop, right_on='Country Name', left_on='name')


#visualize correlation for languages

plt.figure(figsize=(12,10))
sns.heatmap(df_wiki_ratio.corr(), annot=True, vmin=0.80000, vmax=1.00000,fmt='f')


#visualize groups by languages

fig, axs = plt.subplots(nrows=2, ncols=3, figsize=(20, 20))
df_wiki_ratio['ratio_Articles'].sort_values().tail(5).plot.barh(ax=axs[0,0])
axs[0,0].set_xlabel('Articles')
df_wiki_ratio['ratio_Total'].sort_values().tail(5).plot.barh(ax=axs[1,0])
axs[1,0].set_xlabel('Totaş')
df_wiki_ratio['ratio_Edits'].sort_values().tail(5).plot.barh(ax=axs[0,1])
axs[0,1].set_xlabel('Edits')
df_wiki_ratio['ratio_Admins'].sort_values().tail(5).plot.barh(ax=axs[1,1])
axs[1,1].set_xlabel('Admins')
df_wiki_ratio['ratio_Users'].sort_values().tail(5).plot.barh(ax=axs[0,2])
axs[0,2].set_xlabel('Users')
df_wiki_ratio['ratio_Active_Users'].sort_values().tail(5).plot.barh(ax=axs[1,2])
axs[1,2].set_xlabel('Active Users')
plt.tight_layout()


Some insights:

1) In order to access ready data, I used Wikipedia tables, and github repositories

2) There are many entries in those languages although they do not appear first languages for the countries, such as Cebuano. 

3) The correlation between Admins and Articles is high for row dataset. 

4) For world languages, such as English, there are a significant amount of entries. Since they are spoken from different countries and nations, those numbers may mislead us to understand some insights. In order to cope with this problem, it is divided into the total population of countries, in which their given first languages in the dataset respectively. Moreover some small countries are eliminated to get better understandings for big countries 

	4.1) By dividing the population, some world languages lose their power as compare to row dates. 

	4.2) Since it is only one language for each country, it causes dropping for many languages around the world, such as Cebuan . On the other hand, it also shows the importance of citizens living in other countries, such as Catalans. 

	4.3) When it is all a dataset taken into consideration, the correlation among the variables is quite high. On the other hand, ratio of Admins loses its significant for the countries having more than one million population

5) To normalize data by dividing with the population also might not give us fully what we want to learn from the dataset, since there are huge income differences among countries. Therefore values from Wikipedia entry dataset are divided to mean of countries GDP per capita, in which their given first languages in dataset accordingly 

	5.1) By dividing gdp per capita, the picture is quite different from the population table, some of the world languages appear again in the first places. 

	5.2) Moreover, some Southeast Asian countries also climb many stairs with their bigger population sizes and relatively lower gdp per capitas. 

	5.2)  When it is all dataset taken into consideration, the correlation among the variable quite low. On the oher hand, ratio of Admins gains its significany for the countries having more o four tounsend dollars gdp per capita. 
 




