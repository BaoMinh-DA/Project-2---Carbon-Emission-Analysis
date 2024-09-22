

![image](https://github.com/user-attachments/assets/450dec72-db2e-475e-8fb5-e28b94c50448)

What is the project about?


This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.
STEP 1: Which products contribute the most to carbon emissions?

SELECT product_name AS "PRODUCT NAME" , sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT", COMPANY_NAME
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY product_name
ORDER BY sum(carbon_footprint_pcf) desc LIMIT 5

| PRODUCT NAME                 | TOTAL CARBON_FOOTPRINT | COMPANY_NAME                            | 
| ---------------------------: | ---------------------: | --------------------------------------: | 
| Wind Turbine G128 5 Megawats | 3718044                | "Gamesa Corporación Tecnológica, S.A."  | 
| Wind Turbine G132 5 Megawats | 3276187                | "Gamesa Corporación Tecnológica, S.A."  | 
| Wind Turbine G114 2 Megawats | 1532608                | "Gamesa Corporación Tecnológica, S.A."  | 
| Wind Turbine G90 2 Megawats  | 1251625                | "Gamesa Corporación Tecnológica, S.A."  | 
| TCDE                         | 198150                 | "Mitsubishi Gas Chemical Company, Inc." | 
The product that emits the most carbon is Wind Turbine AND THE COMPANY name is "Gamesa Corporación Tecnológica, S.A." 

STEP 2: What are the industry groups of these products?

SELECT product_name AS "PRODUCT NAME" , sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT", COMPANY_NAME, COUNTRY_NAME , industry_group
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY product_name
ORDER BY sum(carbon_footprint_pcf) desc LIMIT 5

| PRODUCT NAME                 | TOTAL CARBON_FOOTPRINT | COMPANY_NAME                            | COUNTRY_NAME | industry_group                     | 
| ---------------------------: | ---------------------: | --------------------------------------: | -----------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats | 3718044                | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats | 3276187                | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats | 1532608                | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats  | 1251625                | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 
| TCDE                         | 198150                 | "Mitsubishi Gas Chemical Company, Inc." | Japan        | Materials                          | 

STEP 3: What are the industries with the highest contribution to carbon emissions?
SELECT  INDUSTRY_GROUP, sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT"
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY industry_group
ORDER BY sum(carbon_footprint_pcf) desc LIMIT 5

| INDUSTRY_GROUP                     | TOTAL CARBON_FOOTPRINT | 
| ---------------------------------: | ---------------------: | 
| Electrical Equipment and Machinery | 9801558                | 
| Automobiles & Components           | 2582264                | 
| Materials                          | 577595                 | 
| Technology Hardware & Equipment    | 363776                 | 
| Capital Goods                      | 258712                 | 



STEP 4: What are the companies with the highest contribution to carbon emissions?
SELECT  COMPANY_NAME, sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT"
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY industry_group
ORDER BY sum(carbon_footprint_pcf) desc LIMIT 5

| COMPANY_NAME                           | TOTAL CARBON_FOOTPRINT | 
| -------------------------------------: | ---------------------: | 
| "Gamesa Corporación Tecnológica, S.A." | 9801558                | 
| "Hino Motors, Ltd."                    | 2582264                | 
| "Kuraray Co., Ltd."                    | 577595                 | 
| "Cisco Systems, Inc."                  | 363776                 | 
| "Daikin Industries, Ltd."              | 258712                 | 

The company with the highest contribution to carbon emissions is "Gamesa Corporación Tecnológica, S.A." 

STEP 5: What are the countries with the highest contribution to carbon emissions?
SELECT  COUNTRY_NAME, sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT"
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY industry_group
ORDER BY sum(carbon_footprint_pcf) desc LIMIT 5

SPAIN is the country that had the highest contribution to the carbon emissions
| COUNTRY_NAME | TOTAL CARBON_FOOTPRINT | 
| -----------: | ---------------------: | 
| Spain        | 9801558                | 
| Japan        | 2582264                | 
| Japan        | 577595                 | 
| USA          | 363776                 | 
| Japan        | 258712                 | 

STEP 6: What is the trend of carbon footprints (PCFs) over the years?

SELECT YEAR, sum(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT"
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY YEAR
ORDER BY YEAR ASC LIMIT 5

| YEAR | TOTAL CARBON_FOOTPRINT | 
| ---: | ---------------------: | 
| 2013 | 503857                 | 
| 2014 | 624226                 | 
| 2015 | 10840415               | 
| 2016 | 1640182                | 
| 2017 | 340271                 | 
Carbon is decrease over the year

STEP 7: Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

SELECT INDUSTRY_GROUP,YEAR, SUM(carbon_footprint_pcf) "TOTAL CARBON_FOOTPRINT"
FROM product_emissions
JOIN companies 		 ON companies.id = product_emissions.company_id
JOIN industry_groups ON industry_groups.id = product_emissions.industry_group_id
JOIN countries 		 ON countries.id = product_emissions.country_id
GROUP BY INDUSTRY_GROUP,YEAR
ORDER BY INDUSTRY_GROUP ASC

| INDUSTRY_GROUP                                                         | YEAR | TOTAL_CARBON_FOOTPRINT | 
| ---------------------------------------------------------------------: | ---: | ---------------------: | 
| "Consumer Durables, Household and Personal Products"                   | 2015 | 931                    | 
| "Food, Beverage & Tobacco"                                             | 2013 | 4995                   | 
| "Food, Beverage & Tobacco"                                             | 2014 | 2685                   | 
| "Food, Beverage & Tobacco"                                             | 2015 | 0                      | 
| "Food, Beverage & Tobacco"                                             | 2016 | 100289                 | 
| "Food, Beverage & Tobacco"                                             | 2017 | 3162                   | 
| "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 2015 | 8909                   | 
| "Mining - Iron, Aluminum, Other Metals"                                | 2015 | 8181                   | 
| "Pharmaceuticals, Biotechnology & Life Sciences"                       | 2013 | 32271                  | 
| "Pharmaceuticals, Biotechnology & Life Sciences"                       | 2014 | 40215                  | 
| "Textiles, Apparel, Footwear and Luxury Goods"                         | 2015 | 387                    | 
| Automobiles & Components                                               | 2013 | 130189                 | 
| Automobiles & Components                                               | 2014 | 230015                 | 
| Automobiles & Components                                               | 2015 | 817227                 | 
| Automobiles & Components                                               | 2016 | 1404833                | 
| Capital Goods                                                          | 2013 | 60190                  | 
| Capital Goods                                                          | 2014 | 93699                  | 
| Capital Goods                                                          | 2015 | 3505                   | 
| Capital Goods                                                          | 2016 | 6369                   | 
| Capital Goods                                                          | 2017 | 94949                  | 
| Chemicals                                                              | 2015 | 62369                  | 
| Commercial & Professional Services                                     | 2013 | 1157                   | 
| Commercial & Professional Services                                     | 2014 | 477                    | 
| Commercial & Professional Services                                     | 2016 | 2890                   | 
| Commercial & Professional Services                                     | 2017 | 741                    | 
| Consumer Durables & Apparel                                            | 2013 | 2867                   | 
| Consumer Durables & Apparel                                            | 2014 | 3280                   | 
| Consumer Durables & Apparel                                            | 2016 | 1162                   | 
| Containers & Packaging                                                 | 2015 | 2988                   | 
| Electrical Equipment and Machinery                                     | 2015 | 9801558                | 
| Energy                                                                 | 2013 | 750                    | 
| Energy                                                                 | 2016 | 10024                  | 
| Food & Beverage Processing                                             | 2015 | 141                    | 
| Food & Staples Retailing                                               | 2014 | 773                    | 
| Food & Staples Retailing                                               | 2015 | 706                    | 
| Food & Staples Retailing                                               | 2016 | 2                      | 
| Gas Utilities                                                          | 2015 | 122                    | 
| Household & Personal Products                                          | 2013 | 0                      | 
| Materials                                                              | 2013 | 200513                 | 
| Materials                                                              | 2014 | 75678                  | 
| Materials                                                              | 2016 | 88267                  | 
| Materials                                                              | 2017 | 213137                 | 
| Media                                                                  | 2013 | 9645                   | 
| Media                                                                  | 2014 | 9645                   | 
| Media                                                                  | 2015 | 1919                   | 
| Media                                                                  | 2016 | 1808                   | 
| Retailing                                                              | 2014 | 19                     | 
| Retailing                                                              | 2015 | 11                     | 
| Semiconductors & Semiconductor Equipment                               | 2014 | 50                     | 
| Semiconductors & Semiconductor Equipment                               | 2016 | 4                      | 
| Semiconductors & Semiconductors Equipment                              | 2015 | 3                      | 
| Software & Services                                                    | 2013 | 6                      | 
| Software & Services                                                    | 2014 | 146                    | 
| Software & Services                                                    | 2015 | 22856                  | 
| Software & Services                                                    | 2016 | 22846                  | 
| Software & Services                                                    | 2017 | 690                    | 
| Technology Hardware & Equipment                                        | 2013 | 61100                  | 
| Technology Hardware & Equipment                                        | 2014 | 167361                 | 
| Technology Hardware & Equipment                                        | 2015 | 106157                 | 
| Technology Hardware & Equipment                                        | 2016 | 1566                   | 
| Technology Hardware & Equipment                                        | 2017 | 27592                  | 
| Telecommunication Services                                             | 2013 | 52                     | 
| Telecommunication Services                                             | 2014 | 183                    | 
| Telecommunication Services                                             | 2015 | 183                    | 
| Tires                                                                  | 2015 | 2022                   | 
| Tobacco                                                                | 2015 | 1                      | 
| Trading Companies & Distributors and Commercial Services & Supplies    | 2015 | 239                    | 
| Utilities                                                              | 2013 | 122                    | 
| Utilities                                                              | 2016 | 122                    | 

"Food, Beverage & Tobacco", Software & Services And Media,Software & Services prove that they can notable decrease in carbon footprints (PCFs) over time.


