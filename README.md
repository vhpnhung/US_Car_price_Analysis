# Car Price in the US Analysis
## Overview
Geely Auto is a Chinese car manufacturing company.
They planned to join the US market by producing their brand-new cars, with an ambition to compete with both domestic and European car brands
## Dataset
The dataset consists of 205 not-null entries, and 27 features as follow:
- car_ID: car identity number
- symboling: Safety estimator (safest: -2, riskiest: 3)
- carName: name of car
- fueltype: fuel used to operate car
- aspiration: aspiration type
- doornumber: number of door
- carbody: body type of car
- drivewheel: type of drivewheel
- enginelocation: location of car engine
- wheelbase: standard car length (calculated by the distance between 2 wheels)
- carlength: length of car
- carwidth: width of car
- carheight: height of car
- curbweight: weight of car curb
- enginetype: type of car engine
- cylindernumber: number of cylinder
- enginesize: size of car engine
- fuelsystem: type of fuel system
- boreratio: car bore-ratio
- stroke: number of stroke
- compressionratio: compression ratio
- horsepower: maximum capacity estimated by HP
- peakrpm: maximum engine speed
- citympg: miles per gallon in city
- highwaympg: miles per gallon on highway
- price: car price
For further analysis, I have added 'CarBrand' feature by extracting from 'carName' feature.
## Summary of Analysis
### Finding 1
![image](https://user-images.githubusercontent.com/108542209/218319608-feb1f837-f940-441f-b4fb-924ce099e0da.png)
- Generally, the majority of cars sold's prices vary from ***$5000 to $10000*** - the low range. Additionally, a considerable price is at over ***$25000***, which means US citizens also favor luxurious cars
### Finding 2
![image](https://user-images.githubusercontent.com/108542209/218319722-d7ec977c-c74c-4c73-bc9a-57a925df8615.png)
- Brands that domain the market share generally have:
    * Average price below the average price of the whole market, except for Volvo & Peugeot (graph 3)
    * Maximum price equal or below the average max price of the whole market, except for Volvo & Nissan (graph 2)
    * Minimum price equal or below the averge min price of the whole market, except for Volvo & Peugeout (group 3)
    * Price range is relatively large, which means they provide cars based on different types of customers - lower limit is noticeably less than min average & upper limit is nearly equal to or less than max average
- Brands that have less market share tend to have extreme prices (extremely low or high), leading to small price ranges  (graph 2)
    * Even if the range is large enough, its limits are either unreacheable (too expensive) or too cheap (which may lead to customers' doubts on quality) (graph 1)
- Volvo appears in many exceptions. Therefore, there might be a secret behind their abnormal pattern. However, in this analysis, that would be ignored.
### Finding 3
By using ```scipy.stats``` to test hypothesis, some conclusions can be made as follow:
- Stroke, Compressionratio and Peakrpm have nothing to do with Price
- Others have relations:
    * MPGs (Citympg, Highwaympg) have NEGATIVE relations with Price, which means: 
        - The less fuel-efficient, the more expensive a car is
    * Others have POSITIVE. Some conclusions:
        - The stronger the car is (based on HP), the more expensive it is. This statement can explain why expensive cars are lack of fuel efficiency
        - The more materials are used to make cars (based on size ratios: wheelbase, carlength, carweight, carheight), the more expensive a car is
        - The more bore-ratio, the more expensive. This statement can explain why expensive cars are much stronger.
### Finding 4
- Cars accelerated by diesel are more expensive than those by gas; therefore, they are harder to sell compared to those by gas
![image](https://user-images.githubusercontent.com/108542209/218320479-2e253e30-f7bc-44e8-8870-ca989b76ff9d.png)

- Carbody has a relatively strong effect on price, since the smallest price difference is even about $2,000
    - Hatchback and Sedan cars domains the market share, thanks to their large price ranges. Additionnally, they are relatively cheap, comparing to Convertible and Hardtop - those are much less sold
![image](https://user-images.githubusercontent.com/108542209/218320507-9b1a084f-ef81-4f37-8b8a-159297c44dcd.png)

- 4wd-drivewheel cars are not favored despite their relatively low price, which is opposite to rwd-drivewheel cars. The reason may lie on price range: while rwd's is approachable for many kinds of customers, 4wd's is not
![image](https://user-images.githubusercontent.com/108542209/218320530-0c3dda03-f265-4472-9f19-c5b3ec1dbc27.png)

- Engine location definitely affects the price. It can be seen that mean price of rear-engine cars is twice as much as that of front-engine cars.
![image](https://user-images.githubusercontent.com/108542209/218320554-87331b2f-7d0a-4a59-bccf-1c8fd0f6d986.png)

- 2 noticeable fuelsystems are 2bbl and mpfi - which are extremely common in the US. Their pattern seems opposite:
    - 2bbl: Lowest price + small price range => Focus on price
    - mpfi: Highest price + large price range => Focus on affordability

- 2-door and 4-door cars's prices seem to have just a little difference
![image](https://user-images.githubusercontent.com/108542209/218320591-b1209f4c-ceef-4daf-83cd-6e80e2aaf2fc.png)
## Machine Learning Model
By using ```sklearn``` library, I have built a basic model in order to predict car price based on 10 most influent features.
I have encoded categorical data by ```get_dummies```, as well as normalized quantitative data before taking it into my model.
I have used ```SelectKBest``` from ```sklearn.feature_selection``` to select 10 best features as above.
OLS Regression model summary is shown as follow:
<img width="512" alt="image" src="https://user-images.githubusercontent.com/108542209/218321231-c47b2a7d-28c5-47c6-94e6-edabf112b7f8.png">

