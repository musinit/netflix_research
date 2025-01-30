# Датасеты


|  Название и ссылка   |   Размер (количество строк)  | Год    | Содержание    |  комментарий   |  Название файла   | 
| --- | --- | --- | --- | --- | --- | 
|  [Kaggle Netflix Movies and TV Show](https://www.kaggle.com/datasets/shivamb/netflix-shows)   | 8000    |  2021   |  название, тип (tv show, series),  режиссер, актеры, страна, длительность (количество сезонов или минуты), категория, возрастной рейтинг, год   |  Можно считать генеральной совокупностью шоу netflix    |   `netflix_titles.csv`  | 
|  [1000 Netflix Show](https://www.kaggle.com/datasets/chasewillden/netflix-shows)   |   1000 (500)  | 2017    |   название, возрастной рейтинг, оценки пользователей, год  |   Датасет для исследования в проекте  |  `NetflixShows.xlsx`   |  
|   [Kaggle Netflix Engagement Report (July to December 2023)](https://www.kaggle.com/datasets/armaanjeetsandhu/netflix-engagement-report-july-to-december-2023)  |  6500   |  2023   |  название, количество просмотров с точностью до 100000, длительность в часах   |   похож на официальный датасет с просмотрами  |  `netflix-engagement-report.csv`   | 
|  [Kaggle Netflix Prize data](https://www.kaggle.com/datasets/netflix-inc/netflix-prize-data)   |   480189x17770  | 2005    |  оценки пользователей для фильмов   | Официальный очень большой датасет для обучения рекомендательной системы    |     | 
|  WIP: Выручка   |     |     |     |     |     | 
|  WIP: оценки IMDb   |     |     |     |     |     |  


## Netflix Movies and TV Shows
Netflix is one of the most popular media and video streaming platforms. They have over 8000 movies or tv shows available on their platform, as of mid-2021, they have over 200M Subscribers globally. This tabular dataset consists of listings of all the movies and tv shows available on Netflix, along with details such as - cast, directors, ratings, release year, duration, etc.

- `show_id` - Unique ID for every Movie / Tv Show
- `type` Identifier - A Movie or TV Show
- `title` Title of the Movie / Tv Show
- `director` - Director of the Movie
- `cast` - Actors involved in the movie / show
- `country` - Country where the movie / show was produced
- `date_added` - Date it was added on Netflix
- `release_year` - Actual Release year of the move / show
- `rating` - TV Rating of the movie / show
- `duration` - Total Duration - in minutes or number of seasons
- `listed_in` - Genere (Documentaries, International TV Shows, TV Dramas, TV Mysteries, ...)
- `description` - The summary description

## 1000 Netflix Show
Способ формирования датасета:

Автор выбрал по 4 фильма из 4х рейтингов (G, PG,  TV-14, TV-MA) и скачал для каждого из 16 фильмов по 53 фильма, рекомендованных нетфликсом.

Мотивация: автор датасета смотрел нетфликс с женой и задумался, стало ли больше шоу рейтинга R и TV-MA?


* `title` - название шоу.
* `rating` - рейтинг шоу. Например: G, PG, TV-14, TV-MA.
* `ratingLevel` - описание рейтинговой группы и особенностей шоу.
* `ratingDescription` - рейтинг шоу, закодированный числом.
* `release year` - год выпуска шоу.
* `user rating score` - оценка пользователей.
* `user rating size` - ? общий рейтинг пользователей.


## Netflix Engagement Report (July to December 2023)

This dataset represents the second edition of What We Watched: A Netflix Engagement Report, covering Netflix viewership from July to December 2023. It captures 99% of all viewing activity on the platform during this period. Since the first edition, Netflix has added runtime and views (calculated as total hours viewed divided by runtime) metrics, as well as separating films and series data.
- `Title` - The name of the Netflix show or movie. Alternative titles were originally included for some movies and shows,
- `Available Globally` - Indicates if the title is available worldwide (Yes/No)
- `Release Date` - The date when the title was released on Netflix (YYYY-MM-DD format)
- `Hours Viewed` - Total number of hours the title was watched by all users. Numbers are formatted with commas as thousands separators, which will need to be
- `Runtime` - The duration of the title (in HH:MM format for series, representing total season length). Asterisk indicates missing or
- `Views` - The number of times the title was viewed, calculated as Hours Viewed divided by Runtime.


## IMBd оценки
IMDb выложили датасеты для некоммерческого использования [dataset](https://developer.imdb.com/non-commercial-datasets/). В них информация примерно об 11 млн фильмов.
Для дополнения нашего датасета использовались:
- `title.basics.tsv.gz` основная информация о фильме
- `title.ratings.tsv.gz` рейтинг фильма
- `title.crew.tsv.gz` id режиссеров и сценаристов фильмов
- `name.basics.tsv.gz` информация о человеке (сценаристе, режиссере)

К сожалению, IMDb не указали доступен ли фильм на платформе netflix, поэтому сначала были объединены датасеты целевой (500 фильмов) и дополнительный (5000 фильмов), а потом к этой таблице была добавлена информация из IMDb. Объединение таблиц проводилось по названию и году выпуска, но эти значения не уникальны (например, бывает фильм и сериал в один год с одним названием). **Все фильмы, для которых возникла неоднозначность, были удалены.**

Полученный датасет назвается `netflix_movies_with_imdb.tsv` и содержит столбцы:
- `title` название фильма
- `release_year` год выпуска
- `rating_small`возрастной рейтинг из маленького целевого датасета
- `user_rating_score` пользовательская оценка из маленького датасета
- `dataset_small` имеет значение small, если фильм с таким названием и годом выпуска есть в маленьком датасете
- `rating_big` возрастной рейтинг из большого датасета
- `type` тип видео из большого датасета
- `dataset_big` имеет значение big, если фильм с таким названием и годом выпуска есть большом датасете
- `director` режиссер из большого датасета
- `score_available` true или false, есть ли пользовательская оценка из маленького датасета
- `dataset` small -только в маленьком датасете, big только в большом, smallbig  в обоих
- `tconst` id фильма в imdb 
- `titleType` тип видео, imdb
- `primaryTitle` название фильма, imdb
- `originalTitle` название фильма на оригинальном языке, imdb
- `isAdult` 0 или 1, imdb
- `startYear` год выпуска, imdb
- `endYear` дата окончания, если применимо, imdb
- `runtimeMinutes` primary runtime of the title, in minutes, imdb
- `genres`  includes up to three genres associated with the title, imdb
- `averageRating` weighted average of all the individual user ratings, imdb
- `numVotes` number of votes the title has received, imdb
- `directors` director(s) of the given title, imdb
- `writers`  writer(s) of the given title, imdb
- `nconst` id режиссера в imdb
- `primaryName` имя режиссера, name by which the person is most often credited
- `birthYear` год рождения режиссера
- `deathYear` год смерти режиссера
- `primaryProfession` the top-3 professions of the person (режиссера)
- `knownForTitles` список id фильмов в базе imdb известных работ режиссера
