# 🌍 World Database Project (MySQL)

A structured relational database project based on a **"World Model"**, built using **MySQL Workbench**. This dataset simulates global demographic, geographic, and economic data—ideal for practicing SQL queries and understanding normalized database structures.

---

## 📌 1. Project Overview

This project involves designing and populating a **relational database** that models global information such as countries, cities, continents, and languages. It serves as a foundation for developing **SQL querying skills**, analyzing real-world data, and simulating international reporting systems.

The project was built using **MySQL Workbench** for data modeling and **MySQL** for schema creation and data management.

---

## 🛠 2. Tools Used

| Tool               | Purpose                                      |
|--------------------|----------------------------------------------|
| **MySQL Workbench**| ER modeling and schema design (`.mwb` file)  |
| **MySQL**          | Query execution and database interaction     |
| **SQL**            | Writing and testing relational queries       |
| **Excel/CSV (optional)** | For importing or exporting sample data     |

---

## 🌐 3. Dataset Overview

The World database includes structured data on:

- 🌎 **Countries** – name, population, region, surface area, etc.
- 🏙️ **Cities** – cities linked to countries with population and location
- 🗺️ **Continents** – global continent reference
- 🗣️ **Languages** – languages spoken in each country and whether they are official
- 💹 **Economy** – GDP and economic indicators (optional expansion)

This dataset simulates a **geopolitical and socio-economic** model used in global data analysis scenarios.

---

## 🧱 4. Schema Overview

The schema includes the following normalized tables:

| Table         | Description                                           |
|---------------|-------------------------------------------------------|
| `continent`   | List of continents (e.g., Europe, Asia)              |
| `country`     | Information about countries including population, area, continent reference |
| `city`        | Cities with foreign key link to `country`            |
| `language`    | Languages spoken in countries, indicating if official |
| `gdp_data` *(optional)* | Economic indicators like GDP, inflation     |

🔗 **Relationships**:
- `country.continent_id → continent.continent_id`
- `city.country_id → country.country_id`
- `language.country_id → country.country_id`

![image](https://github.com/user-attachments/assets/4b4a09cb-cad2-496f-906f-9dd149e0c549)

---

## 📚 5. Key Learnings

- 🔧 How to model real-world entities in a normalized relational schema.
- 📊 Practice writing **JOINs**, **aggregations**, and **filtering** across multiple tables.
- 🧩 Use of **foreign keys** to maintain referential integrity.
- 📥 Experience with data modeling tools (MySQL Workbench `.mwb`) for clean database design.
- 🧠 Simulated a practical dataset useful for education, analysis, and dashboard projects.

---

## 🧪 6. Sample SQL Queries

```sql
-- 1. -- same CountryCode and code
 select CountryCode   
 from city;

-- 2. --Add the Continent
 select country.Name, country.Continent 
 from country
 inner join city
 on country.Code = city.countryCode
 where Continent = "europe"; 

-- 3. -- add AND COUNTRY.NAME="SPAIN", CAPITAL:
 select country.Name, country.Continent, city.name, CAPITAL
 from country
 inner join city
 on country.Code = city.countryCode
 where Continent = "europe" and country.name = "spain";

-- 4. --compiling a list of cities located in Europe from the database to facilitate program planning and student engagement. 
select continent, country.name, city.name
from country
inner join city
on country.code = city.CountryCode
where country.continent in ("europe");

--5. --Scenario: An agricultural research institute is studying countries with low population densities for potential agricultural development projects. 
--  identifying countries with sparse populations from the database to support the institute's research efforts. 
select co.name, ci.Population, co.Population
from country as co
inner join city as ci
on co.code = ci.countrycode
order by co.Population asc
where country.Population <>0;

--6. --TO calculate GNP per city:
select city.name, country.name, country.Population, country.GNP, city.ID,  city.CountryCode, city.population, gnp/city.Population as GNPCITY
from country
inner join city
on country.code = city.countrycode
ORDER BY gnp/city.Population DESC;
