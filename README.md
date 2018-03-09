NICAR18 Tweets
==============
================

-   [Data](#data)
    -   [rtweet](#rtweet)
    -   [Search](#search)
-   [Explore](#explore)
    -   [Tweet frequency over time](#tweet-frequency-over-time)
    -   [Positive/negative sentiment](#positivenegative-sentiment)
    -   [Semantic networks](#semantic-networks)

This is a dedicated repository for tracking [\#NICAR18 tweets](https://twitter.com/hashtag/NICAR18?f=tweets&vertical=default&src=hash) (the official hashtag of 2018 annual Computer-Assisted Reporting Conference).

Data
----

### rtweet

Whether you lookup the status IDs or search/stream new tweets, you'll need to make sure to install the [rtweet](http://rtweet.info) package. The code below will install \[if it's not already\] and load rtweet.

``` r
## install rtweet if not already
if (!requireNamespace("rtweet", quietly = TRUE)) {
  install.packages("rtweet")
}

## load rtweet
library(rtweet)
```

Our data collection method is described in detail below. However, if you want to get straight to the data, simply run the following code:

``` r
## download status IDs file
download.file(
  "https://github.com/computer-assisted-reporting/NICAR18/blob/master/data/search-ids.rds?raw=true",
  "NICAR18_status_ids.rds"
)

## read status IDs fromdownloaded file
ids <- readRDS("NICAR18_status_ids.rds")

## lookup data associated with status ids
rt <- rtweet::lookup_tweets(ids$status_id)
```

### Search

One of the easiest ways to gather Twitter data is to search for the data (using Twitter's REST API). Unlike streaming, searching makes it possible to go back in time. Unfortunately, Twitter sets a rather restrictive cap–roughly nine days–on how far back you can go. Regardless, searching for tweets is often the preferred method. For example, the code below is setup in such a way that it can be executed once \[or even several times\] a day throughout the conference. See the [R code here](R/search.R).

Here's some example code showing what essentially we're doing to collect the data:

``` r
## search terms
nicar18conf <- c("NICAR18", "NICAR2018", "IRE_NICAR")

## search for up to 10,000 tweets mentioning nicar18
rt <- search_tweets(paste(nicar18conf, collapse = " OR "), n = 10000)
```

Explore
-------

To explore the Twitter data, we recommend using the [tidyverse](http://tidyverse.org) packages. We're also using a customized [ggplot2](http://ggplot2.org) theme. See the [R code here](R/tidyggplot.R).

### Tweet frequency over time

To create the image below, the data were summarized into a time series-like data frame and then plotted in order depict the frequency of tweets–aggregated in two-hour intevals–about \#nicar18 over time. See the [R code here](R/ts.R).

<p align="center">
<img width="100%" height="auto" src="img/timefreq.png" />
</p>
 

### Positive/negative sentiment

Next, some sentiment analysis of the tweets so far. See the [R code here](R/sentiment.R).

<p align="center">
<img width="100%" height="auto" src="img/sentiment.png" />
</p>
 

### Semantic networks

The image below depicts a quick and dirty visualization of the semantic network (connections via retweet, quote, mention, or reply) as it is observed in the data. See the [R code here](R/network.R).

<p align="center">
<img width="100%" height="auto" src="img/network.png" />
</p>
 

Ideally, the network visualization would be an interactive, searchable graphic. Since it's not, I've printed out the node size values below.

|  rank| screen\_name                                                        |  log\_n|
|-----:|:--------------------------------------------------------------------|-------:|
|     1| <a href="https://twitter.com/IRE_NICAR">@IRE\_NICAR</a>             |   7.653|
|     2| <a href="https://twitter.com/albertocairo">@albertocairo</a>        |   6.678|
|     3| <a href="https://twitter.com/Danict89">@Danict89</a>                |   5.768|
|     4| <a href="https://twitter.com/itsgeorrge">@itsgeorrge</a>            |   5.474|
|     5| <a href="https://twitter.com/MacDiva">@MacDiva</a>                  |   5.423|
|     6| <a href="https://twitter.com/barbaramaseda">@barbaramaseda</a>      |   5.025|
|     7| <a href="https://twitter.com/martinstabe">@martinstabe</a>          |   4.767|
|     8| <a href="https://twitter.com/sarhutch">@sarhutch</a>                |   4.767|
|     9| <a href="https://twitter.com/asduner">@asduner</a>                  |   4.725|
|    10| <a href="https://twitter.com/DougHaddix">@DougHaddix</a>            |   4.442|
|    11| <a href="https://twitter.com/sharon000">@sharon000</a>              |   4.350|
|    12| <a href="https://twitter.com/dataeditor">@dataeditor</a>            |   4.350|
|    13| <a href="https://twitter.com/myersjustinc">@myersjustinc</a>        |   4.326|
|    14| <a href="https://twitter.com/palewire">@palewire</a>                |   4.254|
|    15| <a href="https://twitter.com/jonkeegan">@jonkeegan</a>              |   4.205|
|    16| <a href="https://twitter.com/LNdata">@LNdata</a>                    |   4.180|
|    17| <a href="https://twitter.com/greglinch">@greglinch</a>              |   4.130|
|    18| <a href="https://twitter.com/JSKstanford">@JSKstanford</a>          |   4.105|
|    19| <a href="https://twitter.com/susannahlocke">@susannahlocke</a>      |   4.105|
|    20| <a href="https://twitter.com/hadleywickham">@hadleywickham</a>      |   4.053|
|    21| <a href="https://twitter.com/carla_astudi">@carla\_astudi</a>       |   4.027|
|    22| <a href="https://twitter.com/PatrickMGarvin">@PatrickMGarvin</a>    |   3.974|
|    23| <a href="https://twitter.com/paldhous">@paldhous</a>                |   3.947|
|    24| <a href="https://twitter.com/Maid_Marianne">@Maid\_Marianne</a>     |   3.920|
|    25| <a href="https://twitter.com/ucbsoj">@ucbsoj</a>                    |   3.864|
|    26| <a href="https://twitter.com/jrue">@jrue</a>                        |   3.808|
|    27| <a href="https://twitter.com/christinezhang">@christinezhang</a>    |   3.779|
|    28| <a href="https://twitter.com/Riogringa">@Riogringa</a>              |   3.721|
|    29| <a href="https://twitter.com/datentaeterin">@datentaeterin</a>      |   3.661|
|    30| <a href="https://twitter.com/jazzmyth">@jazzmyth</a>                |   3.661|
|    31| <a href="https://twitter.com/bymarkwalker">@bymarkwalker</a>        |   3.661|
|    32| <a href="https://twitter.com/losowsky">@losowsky</a>                |   3.631|
|    33| <a href="https://twitter.com/charlesminshew">@charlesminshew</a>    |   3.631|
|    34| <a href="https://twitter.com/rachel_shorey">@rachel\_shorey</a>     |   3.569|
|    35| <a href="https://twitter.com/emamd">@emamd</a>                      |   3.537|
|    36| <a href="https://twitter.com/jeremybowers">@jeremybowers</a>        |   3.537|
|    37| <a href="https://twitter.com/ChadSDay">@ChadSDay</a>                |   3.505|
|    38| <a href="https://twitter.com/merbroussard">@merbroussard</a>        |   3.472|
|    39| <a href="https://twitter.com/ultracasual">@ultracasual</a>          |   3.440|
|    40| <a href="https://twitter.com/NataliaMazotte">@NataliaMazotte</a>    |   3.406|
|    41| <a href="https://twitter.com/charlesornstein">@charlesornstein</a>  |   3.372|
|    42| <a href="https://twitter.com/sarambsimon">@sarambsimon</a>          |   3.338|
|    43| <a href="https://twitter.com/derekeder">@derekeder</a>              |   3.338|
|    44| <a href="https://twitter.com/theboysmithy">@theboysmithy</a>        |   3.303|
|    45| <a href="https://twitter.com/ndiakopoulos">@ndiakopoulos</a>        |   3.267|
|    46| <a href="https://twitter.com/sandhya__k">@sandhya\_\_k</a>          |   3.231|
|    47| <a href="https://twitter.com/SStirling">@SStirling</a>              |   3.231|
|    48| <a href="https://twitter.com/chrisjeavans">@chrisjeavans</a>        |   3.231|
|    49| <a href="https://twitter.com/djordjepadejski">@djordjepadejski</a>  |   3.231|
|    50| <a href="https://twitter.com/cephillips">@cephillips</a>            |   3.195|
|    51| <a href="https://twitter.com/fabiolatorres">@fabiolatorres</a>      |   3.195|
|    52| <a href="https://twitter.com/jonathanstray">@jonathanstray</a>      |   3.195|
|    53| <a href="https://twitter.com/giannagruen">@giannagruen</a>          |   3.195|
|    54| <a href="https://twitter.com/chrishagan">@chrishagan</a>            |   3.195|
|    55| <a href="https://twitter.com/kristinhussey1">@kristinhussey1</a>    |   3.157|
|    56| <a href="https://twitter.com/cjworkbench">@cjworkbench</a>          |   3.157|
|    57| <a href="https://twitter.com/dancow">@dancow</a>                    |   3.119|
|    58| <a href="https://twitter.com/ravenben">@ravenben</a>                |   3.119|
|    59| <a href="https://twitter.com/gebeloffnyt">@gebeloffnyt</a>          |   3.119|
|    60| <a href="https://twitter.com/knightlab">@knightlab</a>              |   3.119|
|    61| <a href="https://twitter.com/kennelliott">@kennelliott</a>          |   3.080|
|    62| <a href="https://twitter.com/nausheenhusain">@nausheenhusain</a>    |   3.080|
|    63| <a href="https://twitter.com/ashlynstill">@ashlynstill</a>          |   3.041|
|    64| <a href="https://twitter.com/haddadme">@haddadme</a>                |   3.041|
|    65| <a href="https://twitter.com/columbiajourn">@columbiajourn</a>      |   3.041|
|    66| <a href="https://twitter.com/JonSCollins">@JonSCollins</a>          |   2.959|
|    67| <a href="https://twitter.com/MaryJoWebster">@MaryJoWebster</a>      |   2.959|
|    68| <a href="https://twitter.com/forestgregg">@forestgregg</a>          |   2.959|
|    69| <a href="https://twitter.com/city_bureau">@city\_bureau</a>         |   2.959|
|    70| <a href="https://twitter.com/lucyparsonslabs">@lucyparsonslabs</a>  |   2.959|
|    71| <a href="https://twitter.com/dataKateR">@dataKateR</a>              |   2.917|
|    72| <a href="https://twitter.com/knightfdn">@knightfdn</a>              |   2.917|
|    73| <a href="https://twitter.com/TimBroderick">@TimBroderick</a>        |   2.917|
|    74| <a href="https://twitter.com/Cezary">@Cezary</a>                    |   2.917|
|    75| <a href="https://twitter.com/JacopoOttaviani">@JacopoOttaviani</a>  |   2.917|
|    76| <a href="https://twitter.com/BrettMmurphy">@BrettMmurphy</a>        |   2.917|
|    77| <a href="https://twitter.com/JoeYerardi">@JoeYerardi</a>            |   2.917|
|    78| <a href="https://twitter.com/fcoel">@fcoel</a>                      |   2.875|
|    79| <a href="https://twitter.com/SophieWarnes">@SophieWarnes</a>        |   2.875|
|    80| <a href="https://twitter.com/KarrieKehoe">@KarrieKehoe</a>          |   2.875|
|    81| <a href="https://twitter.com/molliehanley">@molliehanley</a>        |   2.875|
|    82| <a href="https://twitter.com/eads">@eads</a>                        |   2.875|
|    83| <a href="https://twitter.com/JakeaEkdahl">@JakeaEkdahl</a>          |   2.875|
|    84| <a href="https://twitter.com/fexi">@fexi</a>                        |   2.875|
|    85| <a href="https://twitter.com/internetrebecca">@internetrebecca</a>  |   2.831|
|    86| <a href="https://twitter.com/mgafni">@mgafni</a>                    |   2.831|
|    87| <a href="https://twitter.com/anlugonz">@anlugonz</a>                |   2.831|
|    88| <a href="https://twitter.com/AditiHBhandari">@AditiHBhandari</a>    |   2.831|
|    89| <a href="https://twitter.com/ICFJ">@ICFJ</a>                        |   2.831|
|    90| <a href="https://twitter.com/thomasgpadilla">@thomasgpadilla</a>    |   2.786|
|    91| <a href="https://twitter.com/Disha_RC">@Disha\_RC</a>               |   2.786|
|    92| <a href="https://twitter.com/typodactyl">@typodactyl</a>            |   2.740|
|    93| <a href="https://twitter.com/miriamkp">@miriamkp</a>                |   2.740|
|    94| <a href="https://twitter.com/schwanksta">@schwanksta</a>            |   2.740|
|    95| <a href="https://twitter.com/MJBerens1">@MJBerens1</a>              |   2.692|
|    96| <a href="https://twitter.com/ByJohnRRoby">@ByJohnRRoby</a>          |   2.692|
|    97| <a href="https://twitter.com/mtdukes">@mtdukes</a>                  |   2.692|
|    98| <a href="https://twitter.com/opennews">@opennews</a>                |   2.692|
|    99| <a href="https://twitter.com/_thetextfiles">@\_thetextfiles</a>     |   2.692|
|   100| <a href="https://twitter.com/ProPublica">@ProPublica</a>            |   2.692|
|   101| <a href="https://twitter.com/TowCenter">@TowCenter</a>              |   2.692|
|   102| <a href="https://twitter.com/pickoffwhite">@pickoffwhite</a>        |   2.692|
|   103| <a href="https://twitter.com/stiles">@stiles</a>                    |   2.644|
|   104| <a href="https://twitter.com/euniceylee">@euniceylee</a>            |   2.644|
|   105| <a href="https://twitter.com/DrewOCCRP">@DrewOCCRP</a>              |   2.644|
|   106| <a href="https://twitter.com/91_pometti">@91\_pometti</a>           |   2.644|
|   107| <a href="https://twitter.com/maggiemulvihill">@maggiemulvihill</a>  |   2.644|
|   108| <a href="https://twitter.com/derekwillis">@derekwillis</a>          |   2.644|
|   109| <a href="https://twitter.com/digitalamysw">@digitalamysw</a>        |   2.594|
|   110| <a href="https://twitter.com/fvaraorta">@fvaraorta</a>              |   2.594|
|   111| <a href="https://twitter.com/kearneymw">@kearneymw</a>              |   2.594|
|   112| <a href="https://twitter.com/deldeib">@deldeib</a>                  |   2.594|
|   113| <a href="https://twitter.com/UO_Catalyst">@UO\_Catalyst</a>         |   2.594|
|   114| <a href="https://twitter.com/matt_kiefer">@matt\_kiefer</a>         |   2.594|
|   115| <a href="https://twitter.com/macloo">@macloo</a>                    |   2.542|
|   116| <a href="https://twitter.com/ofadam">@ofadam</a>                    |   2.542|
|   117| <a href="https://twitter.com/iff_or">@iff\_or</a>                   |   2.542|
|   118| <a href="https://twitter.com/_erinmansfield">@\_erinmansfield</a>   |   2.489|
|   119| <a href="https://twitter.com/maxharlow">@maxharlow</a>              |   2.489|
|   120| <a href="https://twitter.com/LaSharah">@LaSharah</a>                |   2.489|
|   121| <a href="https://twitter.com/michelleminkoff">@michelleminkoff</a>  |   2.489|
|   122| <a href="https://twitter.com/NadineSebai">@NadineSebai</a>          |   2.489|
|   123| <a href="https://twitter.com/anieldaniel">@anieldaniel</a>          |   2.489|
|   124| <a href="https://twitter.com/rachelwalexande">@rachelwalexande</a>  |   2.489|
|   125| <a href="https://twitter.com/rararahima">@rararahima</a>            |   2.489|
|   126| <a href="https://twitter.com/IJNet">@IJNet</a>                      |   2.434|
|   127| <a href="https://twitter.com/LoBenichou">@LoBenichou</a>            |   2.434|
|   128| <a href="https://twitter.com/emilywithrow">@emilywithrow</a>        |   2.434|
|   129| <a href="https://twitter.com/KenoyerKelly">@KenoyerKelly</a>        |   2.434|
|   130| <a href="https://twitter.com/hannah_recht">@hannah\_recht</a>       |   2.434|
|   131| <a href="https://twitter.com/zubakskees">@zubakskees</a>            |   2.434|
|   132| <a href="https://twitter.com/jayohday">@jayohday</a>                |   2.434|
|   133| <a href="https://twitter.com/UOsojc">@UOsojc</a>                    |   2.434|
|   134| <a href="https://twitter.com/marc_smith">@marc\_smith</a>           |   2.434|
|   135| <a href="https://twitter.com/sh_devulapalli">@sh\_devulapalli</a>   |   2.434|
|   136| <a href="https://twitter.com/lenifaye">@lenifaye</a>                |   2.434|
|   137| <a href="https://twitter.com/guilherme_amado">@guilherme\_amado</a> |   2.378|
|   138| <a href="https://twitter.com/MadiLAlexander">@MadiLAlexander</a>    |   2.378|
|   139| <a href="https://twitter.com/brianboyer">@brianboyer</a>            |   2.378|
|   140| <a href="https://twitter.com/EscolaDeDados">@EscolaDeDados</a>      |   2.378|
|   141| <a href="https://twitter.com/SamanthaSunne">@SamanthaSunne</a>      |   2.378|
|   142| <a href="https://twitter.com/smr_foundation">@smr\_foundation</a>   |   2.378|
|   143| <a href="https://twitter.com/gerald_arthur">@gerald\_arthur</a>     |   2.378|
|   144| <a href="https://twitter.com/DataMadeCo">@DataMadeCo</a>            |   2.378|
|   145| <a href="https://twitter.com/jbenton">@jbenton</a>                  |   2.378|
|   146| <a href="https://twitter.com/brentajones">@brentajones</a>          |   2.319|
|   147| <a href="https://twitter.com/TWallack">@TWallack</a>                |   2.319|
|   148| <a href="https://twitter.com/NewsbySchmidt">@NewsbySchmidt</a>      |   2.319|
|   149| <a href="https://twitter.com/a_mendelson">@a\_mendelson</a>         |   2.319|
|   150| <a href="https://twitter.com/jeremycaplan">@jeremycaplan</a>        |   2.319|
|   151| <a href="https://twitter.com/elliot_bentley">@elliot\_bentley</a>   |   2.319|
|   152| <a href="https://twitter.com/grovesprof">@grovesprof</a>            |   2.319|
|   153| <a href="https://twitter.com/yoli_martinez">@yoli\_martinez</a>     |   2.319|
|   154| <a href="https://twitter.com/opencorporates">@opencorporates</a>    |   2.319|
|   155| <a href="https://twitter.com/BuildCoffee">@BuildCoffee</a>          |   2.319|
|   156| <a href="https://twitter.com/ToTheVictor">@ToTheVictor</a>          |   2.319|
|   157| <a href="https://twitter.com/CynthFernandez">@CynthFernandez</a>    |   2.319|
|   158| <a href="https://twitter.com/abtran">@abtran</a>                    |   2.319|
|   159| <a href="https://twitter.com/NicoleKDan">@NicoleKDan</a>            |   2.258|
|   160| <a href="https://twitter.com/KCnSunshineJam">@KCnSunshineJam</a>    |   2.258|
|   161| <a href="https://twitter.com/shmcminn">@shmcminn</a>                |   2.258|
|   162| <a href="https://twitter.com/LaurenRohr">@LaurenRohr</a>            |   2.258|
|   163| <a href="https://twitter.com/paulbradshaw">@paulbradshaw</a>        |   2.258|
|   164| <a href="https://twitter.com/RachelleFaroul">@RachelleFaroul</a>    |   2.194|
|   165| <a href="https://twitter.com/JournalismSandy">@JournalismSandy</a>  |   2.194|
|   166| <a href="https://twitter.com/saleemkhan">@saleemkhan</a>            |   2.194|
|   167| <a href="https://twitter.com/morisy">@morisy</a>                    |   2.194|
|   168| <a href="https://twitter.com/beckyyerak">@beckyyerak</a>            |   2.194|
|   169| <a href="https://twitter.com/gufalei">@gufalei</a>                  |   2.194|
|   170| <a href="https://twitter.com/nwatzman">@nwatzman</a>                |   2.194|
|   171| <a href="https://twitter.com/nickswyter">@nickswyter</a>            |   2.194|
|   172| <a href="https://twitter.com/dhmontgomery">@dhmontgomery</a>        |   2.194|
|   173| <a href="https://twitter.com/JournoKateH">@JournoKateH</a>          |   2.194|
|   174| <a href="https://twitter.com/CaitMcGlade">@CaitMcGlade</a>          |   2.194|
|   175| <a href="https://twitter.com/otraletra">@otraletra</a>              |   2.194|
|   176| <a href="https://twitter.com/MikeStucka">@MikeStucka</a>            |   2.127|
|   177| <a href="https://twitter.com/songbogong">@songbogong</a>            |   2.127|
|   178| <a href="https://twitter.com/bugsact">@bugsact</a>                  |   2.127|
|   179| <a href="https://twitter.com/pinardag">@pinardag</a>                |   2.127|
|   180| <a href="https://twitter.com/TishaESPN">@TishaESPN</a>              |   2.127|
|   181| <a href="https://twitter.com/khantasha">@khantasha</a>              |   2.127|
|   182| <a href="https://twitter.com/kleinmatic">@kleinmatic</a>            |   2.127|
|   183| <a href="https://twitter.com/Gregatao">@Gregatao</a>                |   2.127|
|   184| <a href="https://twitter.com/bcumedia">@bcumedia</a>                |   2.127|
|   185| <a href="https://twitter.com/JoeGermuska">@JoeGermuska</a>          |   2.127|
|   186| <a href="https://twitter.com/npenzenstadler">@npenzenstadler</a>    |   2.127|
|   187| <a href="https://twitter.com/AxiosVisuals">@AxiosVisuals</a>        |   2.127|
|   188| <a href="https://twitter.com/akesslerdc">@akesslerdc</a>            |   2.057|
|   189| <a href="https://twitter.com/Ukingsdata">@Ukingsdata</a>            |   2.057|
|   190| <a href="https://twitter.com/msanchezMIA">@msanchezMIA</a>          |   2.057|
|   191| <a href="https://twitter.com/walt_jw">@walt\_jw</a>                 |   2.057|
|   192| <a href="https://twitter.com/mpiccorossi">@mpiccorossi</a>          |   2.057|
|   193| <a href="https://twitter.com/JohnMuyskens">@JohnMuyskens</a>        |   2.057|
|   194| <a href="https://twitter.com/NYTInteractive">@NYTInteractive</a>    |   2.057|
|   195| <a href="https://twitter.com/jordanrau">@jordanrau</a>              |   1.983|
|   196| <a href="https://twitter.com/jasongrotto">@jasongrotto</a>          |   1.983|
|   197| <a href="https://twitter.com/amber_waves">@amber\_waves</a>         |   1.983|
|   198| <a href="https://twitter.com/Lindenberger">@Lindenberger</a>        |   1.983|
|   199| <a href="https://twitter.com/JadJaffar">@JadJaffar</a>              |   1.983|
|   200| <a href="https://twitter.com/ericuman">@ericuman</a>                |   1.983|
|   201| <a href="https://twitter.com/mack_oxenden">@mack\_oxenden</a>       |   1.983|
|   202| <a href="https://twitter.com/TaylorJHartz">@TaylorJHartz</a>        |   1.983|
|   203| <a href="https://twitter.com/WSJGraphics">@WSJGraphics</a>          |   1.983|
|   204| <a href="https://twitter.com/nicoledahmen">@nicoledahmen</a>        |   1.983|
|   205| <a href="https://twitter.com/cbaxter1">@cbaxter1</a>                |   1.983|
|   206| <a href="https://twitter.com/br_data">@br\_data</a>                 |   1.983|
|   207| <a href="https://twitter.com/biffud">@biffud</a>                    |   1.983|
|   208| <a href="https://twitter.com/gregmunno">@gregmunno</a>              |   1.983|
|   209| <a href="https://twitter.com/JOVRNALISM">@JOVRNALISM</a>            |   1.983|
|   210| <a href="https://twitter.com/ChiDM">@ChiDM</a>                      |   1.983|
|   211| <a href="https://twitter.com/ChiAppleseed">@ChiAppleseed</a>        |   1.983|
|   212| <a href="https://twitter.com/wardrachel">@wardrachel</a>            |   1.905|
|   213| <a href="https://twitter.com/robertrdenton">@robertrdenton</a>      |   1.905|
|   214| <a href="https://twitter.com/hunter_owens">@hunter\_owens</a>       |   1.905|
|   215| <a href="https://twitter.com/citizenkrans">@citizenkrans</a>        |   1.905|
|   216| <a href="https://twitter.com/rcfp">@rcfp</a>                        |   1.905|
|   217| <a href="https://twitter.com/sarahalvarezMI">@sarahalvarezMI</a>    |   1.905|
|   218| <a href="https://twitter.com/HilkeSchellmann">@HilkeSchellmann</a>  |   1.905|
|   219| <a href="https://twitter.com/j_la28">@j\_la28</a>                   |   1.905|
|   220| <a href="https://twitter.com/journtoolbox">@journtoolbox</a>        |   1.905|
|   221| <a href="https://twitter.com/LeilaHaddou">@LeilaHaddou</a>          |   1.905|
|   222| <a href="https://twitter.com/joemurph">@joemurph</a>                |   1.905|
|   223| <a href="https://twitter.com/DK_NewsData">@DK\_NewsData</a>         |   1.822|
|   224| <a href="https://twitter.com/Fvjones">@Fvjones</a>                  |   1.822|
|   225| <a href="https://twitter.com/MateoClarke">@MateoClarke</a>          |   1.822|
|   226| <a href="https://twitter.com/PBienenfeld">@PBienenfeld</a>          |   1.822|
|   227| <a href="https://twitter.com/Orla_McCaffrey">@Orla\_McCaffrey</a>   |   1.822|
|   228| <a href="https://twitter.com/nassos_">@nassos\_</a>                 |   1.822|
|   229| <a href="https://twitter.com/Lmazade">@Lmazade</a>                  |   1.822|
|   230| <a href="https://twitter.com/allisonsross">@allisonsross</a>        |   1.822|
|   231| <a href="https://twitter.com/mizamudio">@mizamudio</a>              |   1.822|
|   232| <a href="https://twitter.com/mbgerring">@mbgerring</a>              |   1.822|
|   233| <a href="https://twitter.com/tylerallyndavis">@tylerallyndavis</a>  |   1.822|
|   234| <a href="https://twitter.com/jhett93">@jhett93</a>                  |   1.822|
|   235| <a href="https://twitter.com/magiccia">@magiccia</a>                |   1.822|
|   236| <a href="https://twitter.com/MargotWilliams">@MargotWilliams</a>    |   1.822|
|   237| <a href="https://twitter.com/john_diedrich">@john\_diedrich</a>     |   1.822|
|   238| <a href="https://twitter.com/jonahshai">@jonahshai</a>              |   1.822|
|   239| <a href="https://twitter.com/CraigPalosky">@CraigPalosky</a>        |   1.732|
|   240| <a href="https://twitter.com/txtianmiller">@txtianmiller</a>        |   1.732|
|   241| <a href="https://twitter.com/cherylwt">@cherylwt</a>                |   1.732|
|   242| <a href="https://twitter.com/ahofschneider">@ahofschneider</a>      |   1.732|
|   243| <a href="https://twitter.com/jpheasly">@jpheasly</a>                |   1.732|
|   244| <a href="https://twitter.com/SooOh">@SooOh</a>                      |   1.732|
|   245| <a href="https://twitter.com/tiffehr">@tiffehr</a>                  |   1.732|
|   246| <a href="https://twitter.com/irworkshop">@irworkshop</a>            |   1.732|
|   247| <a href="https://twitter.com/kschorsch">@kschorsch</a>              |   1.732|
|   248| <a href="https://twitter.com/darlacameron">@darlacameron</a>        |   1.732|
|   249| <a href="https://twitter.com/ajmnoble">@ajmnoble</a>                |   1.732|
|   250| <a href="https://twitter.com/Carlapedret">@Carlapedret</a>          |   1.732|
|   251| <a href="https://twitter.com/mcrosasb">@mcrosasb</a>                |   1.732|
|   252| <a href="https://twitter.com/BritRenee_">@BritRenee\_</a>           |   1.732|
|   253| <a href="https://twitter.com/momiperalta">@momiperalta</a>          |   1.732|
|   254| <a href="https://twitter.com/abbyblachman">@abbyblachman</a>        |   1.732|
|   255| <a href="https://twitter.com/ByNinaMartin">@ByNinaMartin</a>        |   1.732|
|   256| <a href="https://twitter.com/davidherzog">@davidherzog</a>          |   1.732|
|   257| <a href="https://twitter.com/DanielTrielli">@DanielTrielli</a>      |   1.636|
|   258| <a href="https://twitter.com/rwells1961">@rwells1961</a>            |   1.636|
|   259| <a href="https://twitter.com/cthydng">@cthydng</a>                  |   1.636|
|   260| <a href="https://twitter.com/MUOBrien">@MUOBrien</a>                |   1.636|
|   261| <a href="https://twitter.com/MUCollegeofComm">@MUCollegeofComm</a>  |   1.636|
|   262| <a href="https://twitter.com/elthenerd">@elthenerd</a>              |   1.636|
|   263| <a href="https://twitter.com/katchicago">@katchicago</a>            |   1.636|
|   264| <a href="https://twitter.com/JaymeKFraser">@JaymeKFraser</a>        |   1.636|
|   265| <a href="https://twitter.com/slifty">@slifty</a>                    |   1.636|
|   266| <a href="https://twitter.com/SouthSideWeekly">@SouthSideWeekly</a>  |   1.636|
|   267| <a href="https://twitter.com/write_this_way">@write\_this\_way</a>  |   1.636|
|   268| <a href="https://twitter.com/ChicagoReporter">@ChicagoReporter</a>  |   1.636|
|   269| <a href="https://twitter.com/justinJprice">@justinJprice</a>        |   1.636|
|   270| <a href="https://twitter.com/salcedonews">@salcedonews</a>          |   1.531|
|   271| <a href="https://twitter.com/mfederis">@mfederis</a>                |   1.531|
|   272| <a href="https://twitter.com/jeanhuguesroy">@jeanhuguesroy</a>      |   1.531|
|   273| <a href="https://twitter.com/garveymcvg">@garveymcvg</a>            |   1.531|
|   274| <a href="https://twitter.com/ICFJKnight">@ICFJKnight</a>            |   1.531|
|   275| <a href="https://twitter.com/MeghanHoyer">@MeghanHoyer</a>          |   1.531|
|   276| <a href="https://twitter.com/LATdatadesk">@LATdatadesk</a>          |   1.531|
|   277| <a href="https://twitter.com/databyler">@databyler</a>              |   1.531|
|   278| <a href="https://twitter.com/amayaverde">@amayaverde</a>            |   1.531|
|   279| <a href="https://twitter.com/Dinsmore">@Dinsmore</a>                |   1.531|
|   280| <a href="https://twitter.com/BradQSkillman">@BradQSkillman</a>      |   1.531|
|   281| <a href="https://twitter.com/SunFoundation">@SunFoundation</a>      |   1.531|
|   282| <a href="https://twitter.com/DJNF">@DJNF</a>                        |   1.531|
|   283| <a href="https://twitter.com/EvanWyloge">@EvanWyloge</a>            |   1.414|
|   284| <a href="https://twitter.com/ChristyGutowsk1">@ChristyGutowsk1</a>  |   1.414|
|   285| <a href="https://twitter.com/myersnews">@myersnews</a>              |   1.414|
|   286| <a href="https://twitter.com/MuckRock">@MuckRock</a>                |   1.414|
|   287| <a href="https://twitter.com/cocteau">@cocteau</a>                  |   1.414|
|   288| <a href="https://twitter.com/gluissandoval">@gluissandoval</a>      |   1.414|
|   289| <a href="https://twitter.com/ReporterTopher">@ReporterTopher</a>    |   1.414|
|   290| <a href="https://twitter.com/UlrikBaltzer">@UlrikBaltzer</a>        |   1.414|
|   291| <a href="https://twitter.com/InfoAmazonia">@InfoAmazonia</a>        |   1.414|
|   292| <a href="https://twitter.com/ashhwu">@ashhwu</a>                    |   1.414|
|   293| <a href="https://twitter.com/gridinoc">@gridinoc</a>                |   1.414|
|   294| <a href="https://twitter.com/Dataminr">@Dataminr</a>                |   1.414|
|   295| <a href="https://twitter.com/bpopken">@bpopken</a>                  |   1.414|
|   296| <a href="https://twitter.com/NiemanLab">@NiemanLab</a>              |   1.414|
|   297| <a href="https://twitter.com/ElenaFerrarin">@ElenaFerrarin</a>      |   1.414|
|   298| <a href="https://twitter.com/mattdrange">@mattdrange</a>            |   1.414|
|   299| <a href="https://twitter.com/carlosrvirgen">@carlosrvirgen</a>      |   1.414|
|   300| <a href="https://twitter.com/EvaConstantaras">@EvaConstantaras</a>  |   1.282|
|   301| <a href="https://twitter.com/DiannaNanez">@DiannaNanez</a>          |   1.282|
|   302| <a href="https://twitter.com/mvtopic">@mvtopic</a>                  |   1.282|
|   303| <a href="https://twitter.com/KenichiSerino">@KenichiSerino</a>      |   1.282|
|   304| <a href="https://twitter.com/pilhofer">@pilhofer</a>                |   1.282|
|   305| <a href="https://twitter.com/act_rational">@act\_rational</a>       |   1.282|
|   306| <a href="https://twitter.com/pierreconti">@pierreconti</a>          |   1.282|
|   307| <a href="https://twitter.com/Mapbox">@Mapbox</a>                    |   1.282|
|   308| <a href="https://twitter.com/IAmStevenPotter">@IAmStevenPotter</a>  |   1.282|
|   309| <a href="https://twitter.com/SPIEGEL_Data">@SPIEGEL\_Data</a>       |   1.282|
|   310| <a href="https://twitter.com/zehnzehen">@zehnzehen</a>              |   1.282|
|   311| <a href="https://twitter.com/JacobNierenberg">@JacobNierenberg</a>  |   1.282|
|   312| <a href="https://twitter.com/nostarch">@nostarch</a>                |   1.282|
|   313| <a href="https://twitter.com/practicalsql">@practicalsql</a>        |   1.282|
|   314| <a href="https://twitter.com/AlenaMaschke">@AlenaMaschke</a>        |   1.282|
|   315| <a href="https://twitter.com/21stShow">@21stShow</a>                |   1.282|
|   316| <a href="https://twitter.com/LeeVGaines">@LeeVGaines</a>            |   1.282|
|   317| <a href="https://twitter.com/ssdatar">@ssdatar</a>                  |   1.282|
|   318| <a href="https://twitter.com/GarrettSantora">@GarrettSantora</a>    |   1.282|
|   319| <a href="https://twitter.com/neo4j">@neo4j</a>                      |   1.282|
|   320| <a href="https://twitter.com/becca_aa">@becca\_aa</a>               |   1.282|
|   321| <a href="https://twitter.com/nhannahjones">@nhannahjones</a>        |   1.129|
|   322| <a href="https://twitter.com/mattwynn">@mattwynn</a>                |   1.129|
|   323| <a href="https://twitter.com/AgNews_Otto">@AgNews\_Otto</a>         |   1.129|
|   324| <a href="https://twitter.com/jburnmurdoch">@jburnmurdoch</a>        |   1.129|
|   325| <a href="https://twitter.com/DagmedyaVeri">@DagmedyaVeri</a>        |   1.129|
|   326| <a href="https://twitter.com/edbice">@edbice</a>                    |   1.129|
|   327| <a href="https://twitter.com/gijnAfrica">@gijnAfrica</a>            |   1.129|
|   328| <a href="https://twitter.com/FedorZarkhin">@FedorZarkhin</a>        |   1.129|
|   329| <a href="https://twitter.com/RobertMaguire_">@RobertMaguire\_</a>   |   1.129|
|   330| <a href="https://twitter.com/JacquieEli">@JacquieEli</a>            |   1.129|
|   331| <a href="https://twitter.com/realavivahr">@realavivahr</a>          |   1.129|
|   332| <a href="https://twitter.com/ChrisLKellerLAT">@ChrisLKellerLAT</a>  |   1.129|
|   333| <a href="https://twitter.com/portlandmercury">@portlandmercury</a>  |   1.129|
|   334| <a href="https://twitter.com/digiphile">@digiphile</a>              |   1.129|
|   335| <a href="https://twitter.com/kcecireyes">@kcecireyes</a>            |   1.129|
|   336| <a href="https://twitter.com/abraji">@abraji</a>                    |   1.129|
|   337| <a href="https://twitter.com/RobertBenincasa">@RobertBenincasa</a>  |   1.129|
|   338| <a href="https://twitter.com/BBGVisualData">@BBGVisualData</a>      |   1.129|
|   339| <a href="https://twitter.com/zammagazine">@zammagazine</a>          |   1.129|
|   340| <a href="https://twitter.com/jczamora">@jczamora</a>                |   1.129|
|   341| <a href="https://twitter.com/StefanieMurray">@StefanieMurray</a>    |   1.129|
|   342| <a href="https://twitter.com/niemanfdn">@niemanfdn</a>              |   0.944|
|   343| <a href="https://twitter.com/MattCData">@MattCData</a>              |   0.944|
|   344| <a href="https://twitter.com/allyjarmanning">@allyjarmanning</a>    |   0.944|
|   345| <a href="https://twitter.com/shansquared">@shansquared</a>          |   0.944|
|   346| <a href="https://twitter.com/kissane">@kissane</a>                  |   0.944|
|   347| <a href="https://twitter.com/wwrfd">@wwrfd</a>                      |   0.702|
|   348| <a href="https://twitter.com/gteresa">@gteresa</a>                  |   0.702|
|   349| <a href="https://twitter.com/tylrfishr">@tylrfishr</a>              |   0.702|
|   350| <a href="https://twitter.com/DDJ_Tools">@DDJ\_Tools</a>             |   0.702|
|   351| <a href="https://twitter.com/tkb">@tkb</a>                          |   0.702|
|   352| <a href="https://twitter.com/thejessicabrady">@thejessicabrady</a>  |   0.702|
|   353| <a href="https://twitter.com/queenalma19">@queenalma19</a>          |   0.702|
|   354| <a href="https://twitter.com/stephanierlamm">@stephanierlamm</a>    |   0.702|
|   355| <a href="https://twitter.com/Brizzyc">@Brizzyc</a>                  |   0.702|
|   356| <a href="https://twitter.com/GerryLanosga">@GerryLanosga</a>        |   0.702|
|   357| <a href="https://twitter.com/zuckerco">@zuckerco</a>                |   0.702|
|   358| <a href="https://twitter.com/crit">@crit</a>                        |   0.702|
|   359| <a href="https://twitter.com/asincopado">@asincopado</a>            |   0.702|
|   360| <a href="https://twitter.com/UFCJCLibrarian">@UFCJCLibrarian</a>    |   0.702|
|   361| <a href="https://twitter.com/gijnArabic">@gijnArabic</a>            |   0.333|
|   362| <a href="https://twitter.com/DanJFord">@DanJFord</a>                |   0.333|
|   363| <a href="https://twitter.com/disolis">@disolis</a>                  |   0.333|
|   364| <a href="https://twitter.com/joemfox">@joemfox</a>                  |   0.333|
|   365| <a href="https://twitter.com/MMInvestigates">@MMInvestigates</a>    |   0.333|
|   366| <a href="https://twitter.com/ReutersPR">@ReutersPR</a>              |   0.333|
|   367| <a href="https://twitter.com/NCDJ_ASU">@NCDJ\_ASU</a>               |   0.333|
|   368| <a href="https://twitter.com/rdmurphy">@rdmurphy</a>                |   0.333|
|   369| <a href="https://twitter.com/noeL_maS">@noeL\_maS</a>               |   0.333|
|   370| <a href="https://twitter.com/mediatwit">@mediatwit</a>              |   0.333|
|   371| <a href="https://twitter.com/MediaShiftOrg">@MediaShiftOrg</a>      |   0.333|
|   372| <a href="https://twitter.com/FrancescaFionda">@FrancescaFionda</a>  |   0.333|
