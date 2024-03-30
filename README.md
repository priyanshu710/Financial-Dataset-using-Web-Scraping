# Financial-Dataset-using-Web-Scraping

The files present in this repository can be used to generate a dataset containing financial information about Indian companies. The data is scraped from the MoneyControl website and then processed to achieve the desired result.

There are 7 different ipynb files needed to achieve the final dataset. You have to run the files in the following order:
    get_links_for_companies.ipynb | 
    Financial_Feature_Extractor.ipynb | 
    merging_data.ipynb | 
    Final_dataset.ipynb | 
    Final_dataset_union.ipynb | 
    adjust_dates.ipynb | 
    include_non_financial_features.ipynb

Now, we shall discuss what each of these files helps us to do.

**get_links_for_companies.ipynb**: We need to get the links to the MoneyControl website of the specific companies we want to get the data for. First of all, make a csv sheet with a column ‘Company Name’ and write down all the companies you need the data for. Then run this file. This file uses google query to search for “{company_name} Share/Stock Price Moneycontrol” and then looks through the initial result that would appear on google and goes inside that website. Then, we look for the financials of the company using some keywords related to the balance sheet. When the link to the balance sheet on Moneycontrol website of the company is found, this is saved in the same csv file. 
But one webpage only contains 5 years of data. So, we go inside this balance sheet link and find the past 5 years of data and save that link separately. These links are for the standalone version of the balance sheet by defaut. So, we repeat the process to search for the consolidated balance sheets. Meanwhile, we are also saving the name of the company we got the weblinks for. This will help us confirm if we have the data for the same company or not. If the links obtained were for a different company than intended, then we can discard that particular result.

**Financial_Feature_Extractor.ipynb**: This file will get the data from the links we collected earlier and save everything in a csv file. In addition to the balance sheets, we also need profit-loss statements, cashflow statements and financial ratios. The links to these statements can be obtained from the balance sheet links. Now, we have 8 links for every company, i.e., 2 links for each different type of statement. We go to each link and scrape the financial statements. In the end, we have 8 files for each company saved in separate folders, where the folder is identified using the name of the company itself.

**merging_data.ipynb**: As we told you earlier, the data for each company is saved in 2 different csv files, each of which contains 5 years of data. The current file will merge both the csv files into a single file. So, we end up with 4 different files for each company.

**Final_dataset.ipynb**: This is where we calculate the financial ratios we need, using the 4 different financial files we prepared earlier. If you want to introduce a new variable, you can do so by understanding how we have calculated the variables and changing the equation according to your desired result.
We will now have the dataset for each company in their specific folders. Remember, the dataset for each company is stored in their specific folders as of now.

**Final_dataset_union.ipynb**: As we still do not have the final dataset with us, we now need to bring the data from all the individual datasets together. The current file helps us do exactly this. This script will take the individual datasets and then merge them into a single file. In the very end, we just transpose the csv file in order to get the feature names on the x-axis, as that is easier to look at.
The dataset will contain 62 financial features at this point.

**adjust_dates.ipynb**: This file will change the datatype of “Year” column to date type. We need to do this because we want to include some other features in the end that are not financials based.

**include_non_financial_features.ipynb**: In a single csv file, we put the information about the ‘Inflation Rate’, ’Unemployement Rate’, ‘Real Interest Rate’ and ‘GDP. Each column contains the respective information from the past several years. We then map this data to the final single dataset we get after merging all the individual datasets.

In the end, we will have the dataset, which contains a total of 66 features. 
