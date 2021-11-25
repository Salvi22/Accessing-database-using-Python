```python
%matplotlib inline
import seaborn
```


```python
!pip install sqlalchemy==1.3.9
```

    Requirement already satisfied: sqlalchemy==1.3.9 in c:\users\anish salvi\anaconda3\lib\site-packages (1.3.9)
    


```python
!pip install ipython-sql
```

    Requirement already satisfied: ipython-sql in c:\users\anish salvi\anaconda3\lib\site-packages (0.4.0)
    Requirement already satisfied: six in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (1.15.0)
    Requirement already satisfied: ipython>=1.0 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (7.19.0)
    Requirement already satisfied: ipython-genutils>=0.1.0 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (0.2.0)
    Requirement already satisfied: prettytable<1 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (0.7.2)
    Requirement already satisfied: sqlalchemy>=0.6.7 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (1.3.9)
    Requirement already satisfied: sqlparse in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython-sql) (0.4.2)
    Requirement already satisfied: colorama; sys_platform == "win32" in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (0.4.4)
    Requirement already satisfied: decorator in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (4.4.2)
    Requirement already satisfied: pickleshare in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (0.7.5)
    Requirement already satisfied: traitlets>=4.2 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (5.0.5)
    Requirement already satisfied: pygments in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (2.7.2)
    Requirement already satisfied: backcall in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (0.2.0)
    Requirement already satisfied: setuptools>=18.5 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (50.3.1.post20201107)
    Requirement already satisfied: jedi>=0.10 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (0.17.1)
    Requirement already satisfied: prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0 in c:\users\anish salvi\anaconda3\lib\site-packages (from ipython>=1.0->ipython-sql) (3.0.8)
    Requirement already satisfied: parso<0.8.0,>=0.7.0 in c:\users\anish salvi\anaconda3\lib\site-packages (from jedi>=0.10->ipython>=1.0->ipython-sql) (0.7.0)
    Requirement already satisfied: wcwidth in c:\users\anish salvi\anaconda3\lib\site-packages (from prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0->ipython>=1.0->ipython-sql) (0.2.5)
    


```python
%load_ext sql
```


```python
%sql ibm_db_sa://vpt69061:lwQxKweEYdWnqArW@98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud:30875/BLUDB?security=SSL
```


```sql
%%sql

CREATE TABLE INTERNATIONAL_STUDENT_TEST_SCORES3 (
	country VARCHAR(50),
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	test_score INT
);
INSERT INTO INTERNATIONAL_STUDENT_TEST_SCORES3 (country, first_name, last_name, test_score)
VALUES
('United States', 'Marshall', 'Bernadot', 54),
('Ghana', 'Celinda', 'Malkin', 51),
('Ukraine', 'Guillermo', 'Furze', 53),
('Greece', 'Aharon', 'Tunnow', 48),
('Russia', 'Bail', 'Goodwin', 46),
('Poland', 'Cole', 'Winteringham', 49),
('Sweden', 'Emlyn', 'Erricker', 55),
('Russia', 'Cathee', 'Sivewright', 49),
('China', 'Barny', 'Ingerson', 57),
('Uganda', 'Sharla', 'Papaccio', 55),
('China', 'Stella', 'Youens', 51),
('Poland', 'Julio', 'Buesden', 48),
('United States', 'Tiffie', 'Cosely', 58),
('Poland', 'Auroora', 'Stiffell', 45),
('China', 'Clarita', 'Huet', 52),
('Poland', 'Shannon', 'Goulden', 45),
('Philippines', 'Emylee', 'Privost', 50),
('France', 'Madelina', 'Burk', 49),
('China', 'Saunderson', 'Root', 58),
('Indonesia', 'Bo', 'Waring', 55),
('China', 'Hollis', 'Domotor', 45),
('Russia', 'Robbie', 'Collip', 46),
('Philippines', 'Davon', 'Donisi', 46),
('China', 'Cristabel', 'Radeliffe', 48),
('China', 'Wallis', 'Bartleet', 58),
('Moldova', 'Arleen', 'Stailey', 38),
('Ireland', 'Mendel', 'Grumble', 58),
('China', 'Sallyann', 'Exley', 51),
('Mexico', 'Kain', 'Swaite', 46),
('Indonesia', 'Alonso', 'Bulteel', 45),
('Armenia', 'Anatol', 'Tankus', 51),
('Indonesia', 'Coralyn', 'Dawkins', 48),
('China', 'Deanne', 'Edwinson', 45),
('China', 'Georgiana', 'Epple', 51),
('Portugal', 'Bartlet', 'Breese', 56),
('Azerbaijan', 'Idalina', 'Lukash', 50),
('France', 'Livvie', 'Flory', 54),
('Malaysia', 'Nonie', 'Borit', 48),
('Indonesia', 'Clio', 'Mugg', 47),
('Brazil', 'Westley', 'Measor', 48),
('Philippines', 'Katrinka', 'Sibbert', 51),
('Poland', 'Valentia', 'Mounch', 50),
('Norway', 'Sheilah', 'Hedditch', 53),
('Papua New Guinea', 'Itch', 'Jubb', 50),
('Latvia', 'Stesha', 'Garnson', 53),
('Canada', 'Cristionna', 'Wadmore', 46),
('China', 'Lianna', 'Gatward', 43),
('Guatemala', 'Tanney', 'Vials', 48),
('France', 'Alma', 'Zavittieri', 44),
('China', 'Alvira', 'Tamas', 50),
('United States', 'Shanon', 'Peres', 45),
('Sweden', 'Maisey', 'Lynas', 53),
('Indonesia', 'Kip', 'Hothersall', 46),
('China', 'Cash', 'Landis', 48),
('Panama', 'Kennith', 'Digance', 45),
('China', 'Ulberto', 'Riggeard', 48),
('Switzerland', 'Judy', 'Gilligan', 49),
('Philippines', 'Tod', 'Trevaskus', 52),
('Brazil', 'Herold', 'Heggs', 44),
('Latvia', 'Verney', 'Note', 50),
('Poland', 'Temp', 'Ribey', 50),
('China', 'Conroy', 'Egdal', 48),
('Japan', 'Gabie', 'Alessandone', 47),
('Ukraine', 'Devlen', 'Chaperlin', 54),
('France', 'Babbette', 'Turner', 51),
('Czech Republic', 'Virgil', 'Scotney', 52),
('Tajikistan', 'Zorina', 'Bedow', 49),
('China', 'Aidan', 'Rudeyeard', 50),
('Ireland', 'Saunder', 'MacLice', 48),
('France', 'Waly', 'Brunstan', 53),
('China', 'Gisele', 'Enns', 52),
('Peru', 'Mina', 'Winchester', 48),
('Japan', 'Torie', 'MacShirrie', 50),
('Russia', 'Benjamen', 'Kenford', 51),
('China', 'Etan', 'Burn', 53),
('Russia', 'Merralee', 'Chaperlin', 38),
('Indonesia', 'Lanny', 'Malam', 49),
('Canada', 'Wilhelm', 'Deeprose', 54),
('Czech Republic', 'Lari', 'Hillhouse', 48),
('China', 'Ossie', 'Woodley', 52),
('Macedonia', 'April', 'Tyer', 50),
('Vietnam', 'Madelon', 'Dansey', 53),
('Ukraine', 'Korella', 'McNamee', 52),
('Jamaica', 'Linnea', 'Cannam', 43),
('China', 'Mart', 'Coling', 52),
('Indonesia', 'Marna', 'Causbey', 47),
('China', 'Berni', 'Daintier', 55),
('Poland', 'Cynthia', 'Hassell', 49),
('Canada', 'Carma', 'Schule', 49),
('Indonesia', 'Malia', 'Blight', 48),
('China', 'Paulo', 'Seivertsen', 47),
('Niger', 'Kaylee', 'Hearley', 54),
('Japan', 'Maure', 'Jandak', 46),
('Argentina', 'Foss', 'Feavers', 45),
('Venezuela', 'Ron', 'Leggitt', 60),
('Russia', 'Flint', 'Gokes', 40),
('China', 'Linet', 'Conelly', 52),
('Philippines', 'Nikolas', 'Birtwell', 57),
('Australia', 'Eduard', 'Leipelt', 53)
```

     * ibm_db_sa://vpt69061:***@98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud:30875/BLUDB
    Done.
    99 rows affected.
    




    []




```python
country = "Canada"
%sql select * from INTERNATIONAL_STUDENT_TEST_SCORES3 where country = :country
```

     * ibm_db_sa://vpt69061:***@98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud:30875/BLUDB
    Done.
    




<table>
    <tr>
        <th>country</th>
        <th>first_name</th>
        <th>last_name</th>
        <th>test_score</th>
    </tr>
    <tr>
        <td>Canada</td>
        <td>Cristionna</td>
        <td>Wadmore</td>
        <td>46</td>
    </tr>
    <tr>
        <td>Canada</td>
        <td>Wilhelm</td>
        <td>Deeprose</td>
        <td>54</td>
    </tr>
    <tr>
        <td>Canada</td>
        <td>Carma</td>
        <td>Schule</td>
        <td>49</td>
    </tr>
</table>




```python
test_score_distribution = %sql SELECT test_score, count(*) as Frequency from INTERNATIONAL_STUDENT_TEST_SCORES3 GROUP BY test_score;
test_score_distribution
```

     * ibm_db_sa://vpt69061:***@98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud:30875/BLUDB
    Done.
    




<table>
    <tr>
        <th>test_score</th>
        <th>frequency</th>
    </tr>
    <tr>
        <td>38</td>
        <td>2</td>
    </tr>
    <tr>
        <td>40</td>
        <td>1</td>
    </tr>
    <tr>
        <td>43</td>
        <td>2</td>
    </tr>
    <tr>
        <td>44</td>
        <td>2</td>
    </tr>
    <tr>
        <td>45</td>
        <td>8</td>
    </tr>
    <tr>
        <td>46</td>
        <td>7</td>
    </tr>
    <tr>
        <td>47</td>
        <td>4</td>
    </tr>
    <tr>
        <td>48</td>
        <td>14</td>
    </tr>
    <tr>
        <td>49</td>
        <td>8</td>
    </tr>
    <tr>
        <td>50</td>
        <td>10</td>
    </tr>
    <tr>
        <td>51</td>
        <td>8</td>
    </tr>
    <tr>
        <td>52</td>
        <td>8</td>
    </tr>
    <tr>
        <td>53</td>
        <td>8</td>
    </tr>
    <tr>
        <td>54</td>
        <td>5</td>
    </tr>
    <tr>
        <td>55</td>
        <td>4</td>
    </tr>
    <tr>
        <td>56</td>
        <td>1</td>
    </tr>
    <tr>
        <td>57</td>
        <td>2</td>
    </tr>
    <tr>
        <td>58</td>
        <td>4</td>
    </tr>
    <tr>
        <td>60</td>
        <td>1</td>
    </tr>
</table>




```python
dataframe = test_score_distribution.DataFrame()
```


```python
%matplotlib inline
```


```python
import seaborn
```


```python

```
