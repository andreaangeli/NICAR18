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
|     1| <a href="https://twitter.com/IRE_NICAR">@IRE\_NICAR</a>             |   8.916|
|     2| <a href="https://twitter.com/Danict89">@Danict89</a>                |   7.182|
|     3| <a href="https://twitter.com/albertocairo">@albertocairo</a>        |   7.146|
|     4| <a href="https://twitter.com/MacDiva">@MacDiva</a>                  |   6.494|
|     5| <a href="https://twitter.com/itsgeorrge">@itsgeorrge</a>            |   6.385|
|     6| <a href="https://twitter.com/susannahlocke">@susannahlocke</a>      |   6.087|
|     7| <a href="https://twitter.com/dataeditor">@dataeditor</a>            |   5.491|
|     8| <a href="https://twitter.com/martinstabe">@martinstabe</a>          |   5.354|
|     9| <a href="https://twitter.com/greglinch">@greglinch</a>              |   5.354|
|    10| <a href="https://twitter.com/hadleywickham">@hadleywickham</a>      |   5.336|
|    11| <a href="https://twitter.com/LNdata">@LNdata</a>                    |   5.301|
|    12| <a href="https://twitter.com/asduner">@asduner</a>                  |   5.301|
|    13| <a href="https://twitter.com/barbaramaseda">@barbaramaseda</a>      |   5.211|
|    14| <a href="https://twitter.com/sandhya__k">@sandhya\_\_k</a>          |   5.044|
|    15| <a href="https://twitter.com/sarhutch">@sarhutch</a>                |   5.025|
|    16| <a href="https://twitter.com/AditiHBhandari">@AditiHBhandari</a>    |   5.006|
|    17| <a href="https://twitter.com/myersjustinc">@myersjustinc</a>        |   4.986|
|    18| <a href="https://twitter.com/JSKstanford">@JSKstanford</a>          |   4.908|
|    19| <a href="https://twitter.com/sharon000">@sharon000</a>              |   4.808|
|    20| <a href="https://twitter.com/charlesornstein">@charlesornstein</a>  |   4.787|
|    21| <a href="https://twitter.com/christinezhang">@christinezhang</a>    |   4.704|
|    22| <a href="https://twitter.com/PatrickMGarvin">@PatrickMGarvin</a>    |   4.641|
|    23| <a href="https://twitter.com/DougHaddix">@DougHaddix</a>            |   4.619|
|    24| <a href="https://twitter.com/palewire">@palewire</a>                |   4.532|
|    25| <a href="https://twitter.com/ucbsoj">@ucbsoj</a>                    |   4.510|
|    26| <a href="https://twitter.com/jonkeegan">@jonkeegan</a>              |   4.465|
|    27| <a href="https://twitter.com/NataliaMazotte">@NataliaMazotte</a>    |   4.373|
|    28| <a href="https://twitter.com/charlesminshew">@charlesminshew</a>    |   4.350|
|    29| <a href="https://twitter.com/Riogringa">@Riogringa</a>              |   4.278|
|    30| <a href="https://twitter.com/dhmontgomery">@dhmontgomery</a>        |   4.254|
|    31| <a href="https://twitter.com/Cezary">@Cezary</a>                    |   4.254|
|    32| <a href="https://twitter.com/iff_or">@iff\_or</a>                   |   4.230|
|    33| <a href="https://twitter.com/paldhous">@paldhous</a>                |   4.205|
|    34| <a href="https://twitter.com/carla_astudi">@carla\_astudi</a>       |   4.205|
|    35| <a href="https://twitter.com/datentaeterin">@datentaeterin</a>      |   4.180|
|    36| <a href="https://twitter.com/jazzmyth">@jazzmyth</a>                |   4.155|
|    37| <a href="https://twitter.com/merbroussard">@merbroussard</a>        |   4.130|
|    38| <a href="https://twitter.com/ultracasual">@ultracasual</a>          |   4.105|
|    39| <a href="https://twitter.com/NewsbySchmidt">@NewsbySchmidt</a>      |   4.105|
|    40| <a href="https://twitter.com/jrue">@jrue</a>                        |   4.105|
|    41| <a href="https://twitter.com/Maid_Marianne">@Maid\_Marianne</a>     |   4.079|
|    42| <a href="https://twitter.com/kbmiami">@kbmiami</a>                  |   4.053|
|    43| <a href="https://twitter.com/LaSharah">@LaSharah</a>                |   4.000|
|    44| <a href="https://twitter.com/otraletra">@otraletra</a>              |   3.974|
|    45| <a href="https://twitter.com/bymarkwalker">@bymarkwalker</a>        |   3.974|
|    46| <a href="https://twitter.com/nausheenhusain">@nausheenhusain</a>    |   3.947|
|    47| <a href="https://twitter.com/dancow">@dancow</a>                    |   3.947|
|    48| <a href="https://twitter.com/fvaraorta">@fvaraorta</a>              |   3.947|
|    49| <a href="https://twitter.com/theboysmithy">@theboysmithy</a>        |   3.947|
|    50| <a href="https://twitter.com/SStirling">@SStirling</a>              |   3.920|
|    51| <a href="https://twitter.com/jonathanstray">@jonathanstray</a>      |   3.892|
|    52| <a href="https://twitter.com/internetrebecca">@internetrebecca</a>  |   3.864|
|    53| <a href="https://twitter.com/AnnaFlagg">@AnnaFlagg</a>              |   3.836|
|    54| <a href="https://twitter.com/ChadSDay">@ChadSDay</a>                |   3.808|
|    55| <a href="https://twitter.com/MaryJoWebster">@MaryJoWebster</a>      |   3.808|
|    56| <a href="https://twitter.com/losowsky">@losowsky</a>                |   3.808|
|    57| <a href="https://twitter.com/knightlab">@knightlab</a>              |   3.808|
|    58| <a href="https://twitter.com/knightfdn">@knightfdn</a>              |   3.808|
|    59| <a href="https://twitter.com/pickoffwhite">@pickoffwhite</a>        |   3.779|
|    60| <a href="https://twitter.com/emamd">@emamd</a>                      |   3.779|
|    61| <a href="https://twitter.com/ProPublica">@ProPublica</a>            |   3.779|
|    62| <a href="https://twitter.com/haddadme">@haddadme</a>                |   3.750|
|    63| <a href="https://twitter.com/jeremycaplan">@jeremycaplan</a>        |   3.750|
|    64| <a href="https://twitter.com/Jeremy_CF_Lin">@Jeremy\_CF\_Lin</a>    |   3.721|
|    65| <a href="https://twitter.com/rachelwalexande">@rachelwalexande</a>  |   3.691|
|    66| <a href="https://twitter.com/city_bureau">@city\_bureau</a>         |   3.691|
|    67| <a href="https://twitter.com/derekeder">@derekeder</a>              |   3.691|
|    68| <a href="https://twitter.com/rachel_shorey">@rachel\_shorey</a>     |   3.691|
|    69| <a href="https://twitter.com/chrishagan">@chrishagan</a>            |   3.661|
|    70| <a href="https://twitter.com/TishaESPN">@TishaESPN</a>              |   3.631|
|    71| <a href="https://twitter.com/areena_arora">@areena\_arora</a>       |   3.631|
|    72| <a href="https://twitter.com/TaylorJHartz">@TaylorJHartz</a>        |   3.631|
|    73| <a href="https://twitter.com/anlugonz">@anlugonz</a>                |   3.631|
|    74| <a href="https://twitter.com/mtdukes">@mtdukes</a>                  |   3.631|
|    75| <a href="https://twitter.com/jeremybowers">@jeremybowers</a>        |   3.631|
|    76| <a href="https://twitter.com/TWallack">@TWallack</a>                |   3.600|
|    77| <a href="https://twitter.com/KarrieKehoe">@KarrieKehoe</a>          |   3.600|
|    78| <a href="https://twitter.com/chrisjeavans">@chrisjeavans</a>        |   3.600|
|    79| <a href="https://twitter.com/JonSCollins">@JonSCollins</a>          |   3.537|
|    80| <a href="https://twitter.com/sarambsimon">@sarambsimon</a>          |   3.537|
|    81| <a href="https://twitter.com/grovesprof">@grovesprof</a>            |   3.537|
|    82| <a href="https://twitter.com/HamdanAzhar">@HamdanAzhar</a>          |   3.505|
|    83| <a href="https://twitter.com/cjworkbench">@cjworkbench</a>          |   3.505|
|    84| <a href="https://twitter.com/djordjepadejski">@djordjepadejski</a>  |   3.440|
|    85| <a href="https://twitter.com/giannagruen">@giannagruen</a>          |   3.440|
|    86| <a href="https://twitter.com/cephillips">@cephillips</a>            |   3.406|
|    87| <a href="https://twitter.com/digiphile">@digiphile</a>              |   3.406|
|    88| <a href="https://twitter.com/ByJohnRRoby">@ByJohnRRoby</a>          |   3.406|
|    89| <a href="https://twitter.com/brentajones">@brentajones</a>          |   3.338|
|    90| <a href="https://twitter.com/mazet">@mazet</a>                      |   3.338|
|    91| <a href="https://twitter.com/schwanksta">@schwanksta</a>            |   3.338|
|    92| <a href="https://twitter.com/ofadam">@ofadam</a>                    |   3.303|
|    93| <a href="https://twitter.com/EvaConstantaras">@EvaConstantaras</a>  |   3.303|
|    94| <a href="https://twitter.com/fabiolatorres">@fabiolatorres</a>      |   3.303|
|    95| <a href="https://twitter.com/edbice">@edbice</a>                    |   3.303|
|    96| <a href="https://twitter.com/jordanrau">@jordanrau</a>              |   3.267|
|    97| <a href="https://twitter.com/ndiakopoulos">@ndiakopoulos</a>        |   3.267|
|    98| <a href="https://twitter.com/gebeloffnyt">@gebeloffnyt</a>          |   3.267|
|    99| <a href="https://twitter.com/derekwillis">@derekwillis</a>          |   3.267|
|   100| <a href="https://twitter.com/marc_smith">@marc\_smith</a>           |   3.267|
|   101| <a href="https://twitter.com/_erinmansfield">@\_erinmansfield</a>   |   3.231|
|   102| <a href="https://twitter.com/derekkravitz">@derekkravitz</a>        |   3.231|
|   103| <a href="https://twitter.com/forestgregg">@forestgregg</a>          |   3.231|
|   104| <a href="https://twitter.com/fcoel">@fcoel</a>                      |   3.195|
|   105| <a href="https://twitter.com/SophieWarnes">@SophieWarnes</a>        |   3.195|
|   106| <a href="https://twitter.com/mjbeckel">@mjbeckel</a>                |   3.195|
|   107| <a href="https://twitter.com/eads">@eads</a>                        |   3.195|
|   108| <a href="https://twitter.com/JakeaEkdahl">@JakeaEkdahl</a>          |   3.195|
|   109| <a href="https://twitter.com/kennelliott">@kennelliott</a>          |   3.195|
|   110| <a href="https://twitter.com/_thetextfiles">@\_thetextfiles</a>     |   3.195|
|   111| <a href="https://twitter.com/nhannahjones">@nhannahjones</a>        |   3.157|
|   112| <a href="https://twitter.com/kristinhussey1">@kristinhussey1</a>    |   3.157|
|   113| <a href="https://twitter.com/dataKateR">@dataKateR</a>              |   3.157|
|   114| <a href="https://twitter.com/shmcminn">@shmcminn</a>                |   3.157|
|   115| <a href="https://twitter.com/cerealcommas">@cerealcommas</a>        |   3.157|
|   116| <a href="https://twitter.com/ravenben">@ravenben</a>                |   3.119|
|   117| <a href="https://twitter.com/ahofschneider">@ahofschneider</a>      |   3.119|
|   118| <a href="https://twitter.com/emilywithrow">@emilywithrow</a>        |   3.119|
|   119| <a href="https://twitter.com/JoeYerardi">@JoeYerardi</a>            |   3.119|
|   120| <a href="https://twitter.com/fexi">@fexi</a>                        |   3.119|
|   121| <a href="https://twitter.com/typodactyl">@typodactyl</a>            |   3.080|
|   122| <a href="https://twitter.com/jayohday">@jayohday</a>                |   3.080|
|   123| <a href="https://twitter.com/ashlynstill">@ashlynstill</a>          |   3.041|
|   124| <a href="https://twitter.com/matt_kiefer">@matt\_kiefer</a>         |   3.041|
|   125| <a href="https://twitter.com/columbiajourn">@columbiajourn</a>      |   3.041|
|   126| <a href="https://twitter.com/j_la28">@j\_la28</a>                   |   3.001|
|   127| <a href="https://twitter.com/cthydng">@cthydng</a>                  |   3.001|
|   128| <a href="https://twitter.com/rararahima">@rararahima</a>            |   3.001|
|   129| <a href="https://twitter.com/abtran">@abtran</a>                    |   3.001|
|   130| <a href="https://twitter.com/maxharlow">@maxharlow</a>              |   2.959|
|   131| <a href="https://twitter.com/TowCenter">@TowCenter</a>              |   2.959|
|   132| <a href="https://twitter.com/ICFJ">@ICFJ</a>                        |   2.959|
|   133| <a href="https://twitter.com/AKSarahB">@AKSarahB</a>                |   2.959|
|   134| <a href="https://twitter.com/Disha_RC">@Disha\_RC</a>               |   2.959|
|   135| <a href="https://twitter.com/JacopoOttaviani">@JacopoOttaviani</a>  |   2.959|
|   136| <a href="https://twitter.com/BrettMmurphy">@BrettMmurphy</a>        |   2.959|
|   137| <a href="https://twitter.com/lucyparsonslabs">@lucyparsonslabs</a>  |   2.959|
|   138| <a href="https://twitter.com/hunter_owens">@hunter\_owens</a>       |   2.917|
|   139| <a href="https://twitter.com/anieldaniel">@anieldaniel</a>          |   2.917|
|   140| <a href="https://twitter.com/journtoolbox">@journtoolbox</a>        |   2.917|
|   141| <a href="https://twitter.com/mattdrange">@mattdrange</a>            |   2.917|
|   142| <a href="https://twitter.com/beckyyerak">@beckyyerak</a>            |   2.917|
|   143| <a href="https://twitter.com/TimBroderick">@TimBroderick</a>        |   2.917|
|   144| <a href="https://twitter.com/a_mendelson">@a\_mendelson</a>         |   2.875|
|   145| <a href="https://twitter.com/msanchezMIA">@msanchezMIA</a>          |   2.875|
|   146| <a href="https://twitter.com/mizzousundevil">@mizzousundevil</a>    |   2.875|
|   147| <a href="https://twitter.com/sarahalvarezMI">@sarahalvarezMI</a>    |   2.875|
|   148| <a href="https://twitter.com/JournoKateH">@JournoKateH</a>          |   2.875|
|   149| <a href="https://twitter.com/carlosrvirgen">@carlosrvirgen</a>      |   2.875|
|   150| <a href="https://twitter.com/kearneymw">@kearneymw</a>              |   2.875|
|   151| <a href="https://twitter.com/HilkeSchellmann">@HilkeSchellmann</a>  |   2.875|
|   152| <a href="https://twitter.com/EscolaDeDados">@EscolaDeDados</a>      |   2.875|
|   153| <a href="https://twitter.com/molliehanley">@molliehanley</a>        |   2.875|
|   154| <a href="https://twitter.com/mgafni">@mgafni</a>                    |   2.831|
|   155| <a href="https://twitter.com/gerald_arthur">@gerald\_arthur</a>     |   2.831|
|   156| <a href="https://twitter.com/MadiLAlexander">@MadiLAlexander</a>    |   2.831|
|   157| <a href="https://twitter.com/jbenton">@jbenton</a>                  |   2.831|
|   158| <a href="https://twitter.com/sh_devulapalli">@sh\_devulapalli</a>   |   2.831|
|   159| <a href="https://twitter.com/CynthFernandez">@CynthFernandez</a>    |   2.786|
|   160| <a href="https://twitter.com/MJBerens1">@MJBerens1</a>              |   2.786|
|   161| <a href="https://twitter.com/euniceylee">@euniceylee</a>            |   2.786|
|   162| <a href="https://twitter.com/thomasgpadilla">@thomasgpadilla</a>    |   2.786|
|   163| <a href="https://twitter.com/MargotWilliams">@MargotWilliams</a>    |   2.786|
|   164| <a href="https://twitter.com/tiffehr">@tiffehr</a>                  |   2.786|
|   165| <a href="https://twitter.com/maggiemulvihill">@maggiemulvihill</a>  |   2.786|
|   166| <a href="https://twitter.com/nassos_">@nassos\_</a>                 |   2.786|
|   167| <a href="https://twitter.com/NadineSebai">@NadineSebai</a>          |   2.786|
|   168| <a href="https://twitter.com/macloo">@macloo</a>                    |   2.740|
|   169| <a href="https://twitter.com/stiles">@stiles</a>                    |   2.740|
|   170| <a href="https://twitter.com/miriamkp">@miriamkp</a>                |   2.740|
|   171| <a href="https://twitter.com/SamanthaSunne">@SamanthaSunne</a>      |   2.740|
|   172| <a href="https://twitter.com/michelleminkoff">@michelleminkoff</a>  |   2.740|
|   173| <a href="https://twitter.com/JohnMuyskens">@JohnMuyskens</a>        |   2.740|
|   174| <a href="https://twitter.com/nickswyter">@nickswyter</a>            |   2.740|
|   175| <a href="https://twitter.com/angshah">@angshah</a>                  |   2.692|
|   176| <a href="https://twitter.com/Gregatao">@Gregatao</a>                |   2.692|
|   177| <a href="https://twitter.com/darlacameron">@darlacameron</a>        |   2.692|
|   178| <a href="https://twitter.com/opennews">@opennews</a>                |   2.692|
|   179| <a href="https://twitter.com/DrewOCCRP">@DrewOCCRP</a>              |   2.644|
|   180| <a href="https://twitter.com/LaurenRohr">@LaurenRohr</a>            |   2.644|
|   181| <a href="https://twitter.com/LoBenichou">@LoBenichou</a>            |   2.644|
|   182| <a href="https://twitter.com/ByNinaMartin">@ByNinaMartin</a>        |   2.644|
|   183| <a href="https://twitter.com/allisonsross">@allisonsross</a>        |   2.644|
|   184| <a href="https://twitter.com/UO_Catalyst">@UO\_Catalyst</a>         |   2.644|
|   185| <a href="https://twitter.com/lenifaye">@lenifaye</a>                |   2.644|
|   186| <a href="https://twitter.com/91_pometti">@91\_pometti</a>           |   2.644|
|   187| <a href="https://twitter.com/deldeib">@deldeib</a>                  |   2.644|
|   188| <a href="https://twitter.com/digitalamysw">@digitalamysw</a>        |   2.594|
|   189| <a href="https://twitter.com/tylrfishr">@tylrfishr</a>              |   2.594|
|   190| <a href="https://twitter.com/JaymeKFraser">@JaymeKFraser</a>        |   2.594|
|   191| <a href="https://twitter.com/elliot_bentley">@elliot\_bentley</a>   |   2.594|
|   192| <a href="https://twitter.com/credcoalition">@credcoalition</a>      |   2.594|
|   193| <a href="https://twitter.com/SunFoundation">@SunFoundation</a>      |   2.594|
|   194| <a href="https://twitter.com/brianboyer">@brianboyer</a>            |   2.594|
|   195| <a href="https://twitter.com/KenichiSerino">@KenichiSerino</a>      |   2.542|
|   196| <a href="https://twitter.com/yoli_martinez">@yoli\_martinez</a>     |   2.542|
|   197| <a href="https://twitter.com/MeghanHoyer">@MeghanHoyer</a>          |   2.542|
|   198| <a href="https://twitter.com/npenzenstadler">@npenzenstadler</a>    |   2.542|
|   199| <a href="https://twitter.com/morisy">@morisy</a>                    |   2.542|
|   200| <a href="https://twitter.com/DataMadeCo">@DataMadeCo</a>            |   2.542|
|   201| <a href="https://twitter.com/ericuman">@ericuman</a>                |   2.542|
|   202| <a href="https://twitter.com/zubakskees">@zubakskees</a>            |   2.542|
|   203| <a href="https://twitter.com/aric_chokey">@aric\_chokey</a>         |   2.542|
|   204| <a href="https://twitter.com/jpeebles">@jpeebles</a>                |   2.489|
|   205| <a href="https://twitter.com/ssktanaka">@ssktanaka</a>              |   2.489|
|   206| <a href="https://twitter.com/lamthuyvo">@lamthuyvo</a>              |   2.489|
|   207| <a href="https://twitter.com/KenoyerKelly">@KenoyerKelly</a>        |   2.489|
|   208| <a href="https://twitter.com/khantasha">@khantasha</a>              |   2.489|
|   209| <a href="https://twitter.com/hannah_recht">@hannah\_recht</a>       |   2.489|
|   210| <a href="https://twitter.com/UOsojc">@UOsojc</a>                    |   2.489|
|   211| <a href="https://twitter.com/IJNet">@IJNet</a>                      |   2.434|
|   212| <a href="https://twitter.com/jkteoh">@jkteoh</a>                    |   2.434|
|   213| <a href="https://twitter.com/JoeGermuska">@JoeGermuska</a>          |   2.434|
|   214| <a href="https://twitter.com/NicoleKDan">@NicoleKDan</a>            |   2.378|
|   215| <a href="https://twitter.com/guilherme_amado">@guilherme\_amado</a> |   2.378|
|   216| <a href="https://twitter.com/adinarayan">@adinarayan</a>            |   2.378|
|   217| <a href="https://twitter.com/susie_c">@susie\_c</a>                 |   2.378|
|   218| <a href="https://twitter.com/levinecarrie">@levinecarrie</a>        |   2.378|
|   219| <a href="https://twitter.com/katchicago">@katchicago</a>            |   2.378|
|   220| <a href="https://twitter.com/ToTheVictor">@ToTheVictor</a>          |   2.378|
|   221| <a href="https://twitter.com/cbaxter1">@cbaxter1</a>                |   2.378|
|   222| <a href="https://twitter.com/smr_foundation">@smr\_foundation</a>   |   2.378|
|   223| <a href="https://twitter.com/DanielTrielli">@DanielTrielli</a>      |   2.319|
|   224| <a href="https://twitter.com/momiperalta">@momiperalta</a>          |   2.319|
|   225| <a href="https://twitter.com/DK_NewsData">@DK\_NewsData</a>         |   2.319|
|   226| <a href="https://twitter.com/wardrachel">@wardrachel</a>            |   2.319|
|   227| <a href="https://twitter.com/songbogong">@songbogong</a>            |   2.319|
|   228| <a href="https://twitter.com/hollyhacker">@hollyhacker</a>          |   2.319|
|   229| <a href="https://twitter.com/LeilaHaddou">@LeilaHaddou</a>          |   2.319|
|   230| <a href="https://twitter.com/pilhofer">@pilhofer</a>                |   2.319|
|   231| <a href="https://twitter.com/ReutersPR">@ReutersPR</a>              |   2.319|
|   232| <a href="https://twitter.com/DDJ_Tools">@DDJ\_Tools</a>             |   2.319|
|   233| <a href="https://twitter.com/OpenSecretsDC">@OpenSecretsDC</a>      |   2.319|
|   234| <a href="https://twitter.com/joemurph">@joemurph</a>                |   2.319|
|   235| <a href="https://twitter.com/opencorporates">@opencorporates</a>    |   2.319|
|   236| <a href="https://twitter.com/BuildCoffee">@BuildCoffee</a>          |   2.319|
|   237| <a href="https://twitter.com/ranjchak">@ranjchak</a>                |   2.258|
|   238| <a href="https://twitter.com/salcedonews">@salcedonews</a>          |   2.258|
|   239| <a href="https://twitter.com/KCnSunshineJam">@KCnSunshineJam</a>    |   2.258|
|   240| <a href="https://twitter.com/mshelton">@mshelton</a>                |   2.258|
|   241| <a href="https://twitter.com/SooOh">@SooOh</a>                      |   2.258|
|   242| <a href="https://twitter.com/heychrisbarr">@heychrisbarr</a>        |   2.258|
|   243| <a href="https://twitter.com/webjournalist">@webjournalist</a>      |   2.258|
|   244| <a href="https://twitter.com/pinardag">@pinardag</a>                |   2.258|
|   245| <a href="https://twitter.com/UlrikBaltzer">@UlrikBaltzer</a>        |   2.258|
|   246| <a href="https://twitter.com/NiemanLab">@NiemanLab</a>              |   2.258|
|   247| <a href="https://twitter.com/CaitMcGlade">@CaitMcGlade</a>          |   2.258|
|   248| <a href="https://twitter.com/paulbradshaw">@paulbradshaw</a>        |   2.258|
|   249| <a href="https://twitter.com/chrisschnaars">@chrisschnaars</a>      |   2.194|
|   250| <a href="https://twitter.com/RachelleFaroul">@RachelleFaroul</a>    |   2.194|
|   251| <a href="https://twitter.com/akesslerdc">@akesslerdc</a>            |   2.194|
|   252| <a href="https://twitter.com/cherylwt">@cherylwt</a>                |   2.194|
|   253| <a href="https://twitter.com/jasongrotto">@jasongrotto</a>          |   2.194|
|   254| <a href="https://twitter.com/JournalismSandy">@JournalismSandy</a>  |   2.194|
|   255| <a href="https://twitter.com/scott2b">@scott2b</a>                  |   2.194|
|   256| <a href="https://twitter.com/gregmunno">@gregmunno</a>              |   2.194|
|   257| <a href="https://twitter.com/cameronhickey">@cameronhickey</a>      |   2.194|
|   258| <a href="https://twitter.com/MuckRock">@MuckRock</a>                |   2.194|
|   259| <a href="https://twitter.com/mpiccorossi">@mpiccorossi</a>          |   2.194|
|   260| <a href="https://twitter.com/saleemkhan">@saleemkhan</a>            |   2.194|
|   261| <a href="https://twitter.com/gufalei">@gufalei</a>                  |   2.194|
|   262| <a href="https://twitter.com/nwatzman">@nwatzman</a>                |   2.194|
|   263| <a href="https://twitter.com/MikeStucka">@MikeStucka</a>            |   2.127|
|   264| <a href="https://twitter.com/bugsact">@bugsact</a>                  |   2.127|
|   265| <a href="https://twitter.com/elthenerd">@elthenerd</a>              |   2.127|
|   266| <a href="https://twitter.com/MoizSyed">@MoizSyed</a>                |   2.127|
|   267| <a href="https://twitter.com/nicoledahmen">@nicoledahmen</a>        |   2.127|
|   268| <a href="https://twitter.com/reginafcompton">@reginafcompton</a>    |   2.127|
|   269| <a href="https://twitter.com/kleinmatic">@kleinmatic</a>            |   2.127|
|   270| <a href="https://twitter.com/bcumedia">@bcumedia</a>                |   2.127|
|   271| <a href="https://twitter.com/AxiosVisuals">@AxiosVisuals</a>        |   2.127|
|   272| <a href="https://twitter.com/ceostroff">@ceostroff</a>              |   2.057|
|   273| <a href="https://twitter.com/Ukingsdata">@Ukingsdata</a>            |   2.057|
|   274| <a href="https://twitter.com/amber_waves">@amber\_waves</a>         |   2.057|
|   275| <a href="https://twitter.com/robertrdenton">@robertrdenton</a>      |   2.057|
|   276| <a href="https://twitter.com/allyjarmanning">@allyjarmanning</a>    |   2.057|
|   277| <a href="https://twitter.com/nixonron">@nixonron</a>                |   2.057|
|   278| <a href="https://twitter.com/pierreconti">@pierreconti</a>          |   2.057|
|   279| <a href="https://twitter.com/JonRMcClure">@JonRMcClure</a>          |   2.057|
|   280| <a href="https://twitter.com/rgibbs">@rgibbs</a>                    |   2.057|
|   281| <a href="https://twitter.com/mizamudio">@mizamudio</a>              |   2.057|
|   282| <a href="https://twitter.com/JeffKLO">@JeffKLO</a>                  |   2.057|
|   283| <a href="https://twitter.com/zhoyoyo">@zhoyoyo</a>                  |   2.057|
|   284| <a href="https://twitter.com/walt_jw">@walt\_jw</a>                 |   2.057|
|   285| <a href="https://twitter.com/NYTInteractive">@NYTInteractive</a>    |   2.057|
|   286| <a href="https://twitter.com/Lindenberger">@Lindenberger</a>        |   1.983|
|   287| <a href="https://twitter.com/JadJaffar">@JadJaffar</a>              |   1.983|
|   288| <a href="https://twitter.com/iaivanova">@iaivanova</a>              |   1.983|
|   289| <a href="https://twitter.com/smfrogers">@smfrogers</a>              |   1.983|
|   290| <a href="https://twitter.com/mbgerring">@mbgerring</a>              |   1.983|
|   291| <a href="https://twitter.com/AlexMahadevan">@AlexMahadevan</a>      |   1.983|
|   292| <a href="https://twitter.com/sfrostenson">@sfrostenson</a>          |   1.983|
|   293| <a href="https://twitter.com/KHNews">@KHNews</a>                    |   1.983|
|   294| <a href="https://twitter.com/rcfp">@rcfp</a>                        |   1.983|
|   295| <a href="https://twitter.com/TTBallantyne">@TTBallantyne</a>        |   1.983|
|   296| <a href="https://twitter.com/SamataJo">@SamataJo</a>                |   1.983|
|   297| <a href="https://twitter.com/shansquared">@shansquared</a>          |   1.983|
|   298| <a href="https://twitter.com/mack_oxenden">@mack\_oxenden</a>       |   1.983|
|   299| <a href="https://twitter.com/WSJGraphics">@WSJGraphics</a>          |   1.983|
|   300| <a href="https://twitter.com/br_data">@br\_data</a>                 |   1.983|
|   301| <a href="https://twitter.com/jonahshai">@jonahshai</a>              |   1.983|
|   302| <a href="https://twitter.com/biffud">@biffud</a>                    |   1.983|
|   303| <a href="https://twitter.com/JOVRNALISM">@JOVRNALISM</a>            |   1.983|
|   304| <a href="https://twitter.com/ChiDM">@ChiDM</a>                      |   1.983|
|   305| <a href="https://twitter.com/ChiAppleseed">@ChiAppleseed</a>        |   1.983|
|   306| <a href="https://twitter.com/Fvjones">@Fvjones</a>                  |   1.905|
|   307| <a href="https://twitter.com/MateoClarke">@MateoClarke</a>          |   1.905|
|   308| <a href="https://twitter.com/citizenkrans">@citizenkrans</a>        |   1.905|
|   309| <a href="https://twitter.com/kavyaSukumar">@kavyaSukumar</a>        |   1.905|
|   310| <a href="https://twitter.com/VigneshR">@VigneshR</a>                |   1.905|
|   311| <a href="https://twitter.com/allthingscensus">@allthingscensus</a>  |   1.905|
|   312| <a href="https://twitter.com/BayAreaData">@BayAreaData</a>          |   1.905|
|   313| <a href="https://twitter.com/nicolelzhu">@nicolelzhu</a>            |   1.905|
|   314| <a href="https://twitter.com/Botometer">@Botometer</a>              |   1.905|
|   315| <a href="https://twitter.com/john_diedrich">@john\_diedrich</a>     |   1.905|
|   316| <a href="https://twitter.com/magiccia">@magiccia</a>                |   1.905|
|   317| <a href="https://twitter.com/truthyatindiana">@truthyatindiana</a>  |   1.822|
|   318| <a href="https://twitter.com/rwells1961">@rwells1961</a>            |   1.822|
|   319| <a href="https://twitter.com/CraigPalosky">@CraigPalosky</a>        |   1.822|
|   320| <a href="https://twitter.com/PBienenfeld">@PBienenfeld</a>          |   1.822|
|   321| <a href="https://twitter.com/Orla_McCaffrey">@Orla\_McCaffrey</a>   |   1.822|
|   322| <a href="https://twitter.com/davidherzog">@davidherzog</a>          |   1.822|
|   323| <a href="https://twitter.com/d_holli">@d\_holli</a>                 |   1.822|
|   324| <a href="https://twitter.com/adventurejason">@adventurejason</a>    |   1.822|
|   325| <a href="https://twitter.com/amandabee">@amandabee</a>              |   1.822|
|   326| <a href="https://twitter.com/DanielPWWood">@DanielPWWood</a>        |   1.822|
|   327| <a href="https://twitter.com/garveymcvg">@garveymcvg</a>            |   1.822|
|   328| <a href="https://twitter.com/SeraMak">@SeraMak</a>                  |   1.822|
|   329| <a href="https://twitter.com/Lmazade">@Lmazade</a>                  |   1.822|
|   330| <a href="https://twitter.com/tylerallyndavis">@tylerallyndavis</a>  |   1.822|
|   331| <a href="https://twitter.com/jhett93">@jhett93</a>                  |   1.822|
|   332| <a href="https://twitter.com/txtianmiller">@txtianmiller</a>        |   1.732|
|   333| <a href="https://twitter.com/jpheasly">@jpheasly</a>                |   1.732|
|   334| <a href="https://twitter.com/jburnmurdoch">@jburnmurdoch</a>        |   1.732|
|   335| <a href="https://twitter.com/BradQSkillman">@BradQSkillman</a>      |   1.732|
|   336| <a href="https://twitter.com/neenahyena">@neenahyena</a>            |   1.732|
|   337| <a href="https://twitter.com/onlyandrewn">@onlyandrewn</a>          |   1.732|
|   338| <a href="https://twitter.com/JacquieEli">@JacquieEli</a>            |   1.732|
|   339| <a href="https://twitter.com/UFJSchool">@UFJSchool</a>              |   1.732|
|   340| <a href="https://twitter.com/cocteau">@cocteau</a>                  |   1.732|
|   341| <a href="https://twitter.com/PaigeBlank">@PaigeBlank</a>            |   1.732|
|   342| <a href="https://twitter.com/asuozzo">@asuozzo</a>                  |   1.732|
|   343| <a href="https://twitter.com/irworkshop">@irworkshop</a>            |   1.732|
|   344| <a href="https://twitter.com/kschorsch">@kschorsch</a>              |   1.732|
|   345| <a href="https://twitter.com/ajmnoble">@ajmnoble</a>                |   1.732|
|   346| <a href="https://twitter.com/Carlapedret">@Carlapedret</a>          |   1.732|
|   347| <a href="https://twitter.com/mcrosasb">@mcrosasb</a>                |   1.732|
|   348| <a href="https://twitter.com/BritRenee_">@BritRenee\_</a>           |   1.732|
|   349| <a href="https://twitter.com/abbyblachman">@abbyblachman</a>        |   1.732|
|   350| <a href="https://twitter.com/jackgillum">@jackgillum</a>            |   1.636|
|   351| <a href="https://twitter.com/chrissiemurray">@chrissiemurray</a>    |   1.636|
|   352| <a href="https://twitter.com/mfederis">@mfederis</a>                |   1.636|
|   353| <a href="https://twitter.com/LATdatadesk">@LATdatadesk</a>          |   1.636|
|   354| <a href="https://twitter.com/DeniseDSLu">@DeniseDSLu</a>            |   1.636|
|   355| <a href="https://twitter.com/JoshKalov">@JoshKalov</a>              |   1.636|
|   356| <a href="https://twitter.com/ICFJKnight">@ICFJKnight</a>            |   1.636|
|   357| <a href="https://twitter.com/MonaChalabi">@MonaChalabi</a>          |   1.636|
|   358| <a href="https://twitter.com/lenagroeger">@lenagroeger</a>          |   1.636|
|   359| <a href="https://twitter.com/IAmStevenPotter">@IAmStevenPotter</a>  |   1.636|
|   360| <a href="https://twitter.com/stephanierlamm">@stephanierlamm</a>    |   1.636|
|   361| <a href="https://twitter.com/AnjeanetteDamon">@AnjeanetteDamon</a>  |   1.636|
|   362| <a href="https://twitter.com/gridinoc">@gridinoc</a>                |   1.636|
|   363| <a href="https://twitter.com/zehnzehen">@zehnzehen</a>              |   1.636|
|   364| <a href="https://twitter.com/databyler">@databyler</a>              |   1.636|
|   365| <a href="https://twitter.com/micahflee">@micahflee</a>              |   1.636|
|   366| <a href="https://twitter.com/kylebentle">@kylebentle</a>            |   1.636|
|   367| <a href="https://twitter.com/MUOBrien">@MUOBrien</a>                |   1.636|
|   368| <a href="https://twitter.com/MUCollegeofComm">@MUCollegeofComm</a>  |   1.636|
|   369| <a href="https://twitter.com/amayaverde">@amayaverde</a>            |   1.636|
|   370| <a href="https://twitter.com/slifty">@slifty</a>                    |   1.636|
|   371| <a href="https://twitter.com/SouthSideWeekly">@SouthSideWeekly</a>  |   1.636|
|   372| <a href="https://twitter.com/write_this_way">@write\_this\_way</a>  |   1.636|
|   373| <a href="https://twitter.com/ChicagoReporter">@ChicagoReporter</a>  |   1.636|
|   374| <a href="https://twitter.com/justinJprice">@justinJprice</a>        |   1.636|
|   375| <a href="https://twitter.com/ChristyGutowsk1">@ChristyGutowsk1</a>  |   1.531|
|   376| <a href="https://twitter.com/jeanhuguesroy">@jeanhuguesroy</a>      |   1.531|
|   377| <a href="https://twitter.com/ProPublicaIL">@ProPublicaIL</a>        |   1.531|
|   378| <a href="https://twitter.com/AlenaMaschke">@AlenaMaschke</a>        |   1.531|
|   379| <a href="https://twitter.com/disolis">@disolis</a>                  |   1.531|
|   380| <a href="https://twitter.com/gilra">@gilra</a>                      |   1.531|
|   381| <a href="https://twitter.com/MattTheJourno">@MattTheJourno</a>      |   1.531|
|   382| <a href="https://twitter.com/JoonParkMusic">@JoonParkMusic</a>      |   1.531|
|   383| <a href="https://twitter.com/niemanfdn">@niemanfdn</a>              |   1.531|
|   384| <a href="https://twitter.com/JacobNierenberg">@JacobNierenberg</a>  |   1.531|
|   385| <a href="https://twitter.com/myersnews">@myersnews</a>              |   1.531|
|   386| <a href="https://twitter.com/lisalsong">@lisalsong</a>              |   1.531|
|   387| <a href="https://twitter.com/gluissandoval">@gluissandoval</a>      |   1.531|
|   388| <a href="https://twitter.com/tylermachado">@tylermachado</a>        |   1.531|
|   389| <a href="https://twitter.com/Dinsmore">@Dinsmore</a>                |   1.531|
|   390| <a href="https://twitter.com/DJNF">@DJNF</a>                        |   1.531|
|   391| <a href="https://twitter.com/RachelSB">@RachelSB</a>                |   1.414|
|   392| <a href="https://twitter.com/EvanWyloge">@EvanWyloge</a>            |   1.414|
|   393| <a href="https://twitter.com/DeniseMalan">@DeniseMalan</a>          |   1.414|
|   394| <a href="https://twitter.com/ssdatar">@ssdatar</a>                  |   1.414|
|   395| <a href="https://twitter.com/act_rational">@act\_rational</a>       |   1.414|
|   396| <a href="https://twitter.com/GurmanBhatia">@GurmanBhatia</a>        |   1.414|
|   397| <a href="https://twitter.com/Vince_Dixon_">@Vince\_Dixon\_</a>      |   1.414|
|   398| <a href="https://twitter.com/rctatman">@rctatman</a>                |   1.414|
|   399| <a href="https://twitter.com/OpenSemSearch">@OpenSemSearch</a>      |   1.414|
|   400| <a href="https://twitter.com/priyakkumar">@priyakkumar</a>          |   1.414|
|   401| <a href="https://twitter.com/FedorZarkhin">@FedorZarkhin</a>        |   1.414|
|   402| <a href="https://twitter.com/JuliaJRH">@JuliaJRH</a>                |   1.414|
|   403| <a href="https://twitter.com/kcrowebasspro">@kcrowebasspro</a>      |   1.414|
|   404| <a href="https://twitter.com/jeremybmerrill">@jeremybmerrill</a>    |   1.414|
|   405| <a href="https://twitter.com/juliasilge">@juliasilge</a>            |   1.414|
|   406| <a href="https://twitter.com/gijnAfrica">@gijnAfrica</a>            |   1.414|
|   407| <a href="https://twitter.com/ReporterTopher">@ReporterTopher</a>    |   1.414|
|   408| <a href="https://twitter.com/InfoAmazonia">@InfoAmazonia</a>        |   1.414|
|   409| <a href="https://twitter.com/ChrisLKellerLAT">@ChrisLKellerLAT</a>  |   1.414|
|   410| <a href="https://twitter.com/ashhwu">@ashhwu</a>                    |   1.414|
|   411| <a href="https://twitter.com/Dataminr">@Dataminr</a>                |   1.414|
|   412| <a href="https://twitter.com/bpopken">@bpopken</a>                  |   1.414|
|   413| <a href="https://twitter.com/ElenaFerrarin">@ElenaFerrarin</a>      |   1.414|
|   414| <a href="https://twitter.com/DiannaNanez">@DiannaNanez</a>          |   1.282|
|   415| <a href="https://twitter.com/nerdishtendency">@nerdishtendency</a>  |   1.282|
|   416| <a href="https://twitter.com/news_klaxon">@news\_klaxon</a>         |   1.282|
|   417| <a href="https://twitter.com/KtTobar">@KtTobar</a>                  |   1.282|
|   418| <a href="https://twitter.com/bikeprof">@bikeprof</a>                |   1.282|
|   419| <a href="https://twitter.com/queenalma19">@queenalma19</a>          |   1.282|
|   420| <a href="https://twitter.com/c_milneil">@c\_milneil</a>             |   1.282|
|   421| <a href="https://twitter.com/HartlandZoe">@HartlandZoe</a>          |   1.282|
|   422| <a href="https://twitter.com/resentfultweet">@resentfultweet</a>    |   1.282|
|   423| <a href="https://twitter.com/CarlieProcell">@CarlieProcell</a>      |   1.282|
|   424| <a href="https://twitter.com/runasand">@runasand</a>                |   1.282|
|   425| <a href="https://twitter.com/mvtopic">@mvtopic</a>                  |   1.282|
|   426| <a href="https://twitter.com/thensim0nsaid">@thensim0nsaid</a>      |   1.282|
|   427| <a href="https://twitter.com/Mapbox">@Mapbox</a>                    |   1.282|
|   428| <a href="https://twitter.com/SPIEGEL_Data">@SPIEGEL\_Data</a>       |   1.282|
|   429| <a href="https://twitter.com/nostarch">@nostarch</a>                |   1.282|
|   430| <a href="https://twitter.com/practicalsql">@practicalsql</a>        |   1.282|
|   431| <a href="https://twitter.com/21stShow">@21stShow</a>                |   1.282|
|   432| <a href="https://twitter.com/LeeVGaines">@LeeVGaines</a>            |   1.282|
|   433| <a href="https://twitter.com/GarrettSantora">@GarrettSantora</a>    |   1.282|
|   434| <a href="https://twitter.com/neo4j">@neo4j</a>                      |   1.282|
|   435| <a href="https://twitter.com/some_yeo">@some\_yeo</a>               |   1.282|
|   436| <a href="https://twitter.com/becca_aa">@becca\_aa</a>               |   1.282|
|   437| <a href="https://twitter.com/UFCJCLibrarian">@UFCJCLibrarian</a>    |   1.129|
|   438| <a href="https://twitter.com/mattwynn">@mattwynn</a>                |   1.129|
|   439| <a href="https://twitter.com/AgNews_Otto">@AgNews\_Otto</a>         |   1.129|
|   440| <a href="https://twitter.com/jsmithrichards">@jsmithrichards</a>    |   1.129|
|   441| <a href="https://twitter.com/crit">@crit</a>                        |   1.129|
|   442| <a href="https://twitter.com/kclarkcollege">@kclarkcollege</a>      |   1.129|
|   443| <a href="https://twitter.com/ipsosus">@ipsosus</a>                  |   1.129|
|   444| <a href="https://twitter.com/thejessicabrady">@thejessicabrady</a>  |   1.129|
|   445| <a href="https://twitter.com/Evie_xing">@Evie\_xing</a>             |   1.129|
|   446| <a href="https://twitter.com/ndungca">@ndungca</a>                  |   1.129|
|   447| <a href="https://twitter.com/GdnMobileLab">@GdnMobileLab</a>        |   1.129|
|   448| <a href="https://twitter.com/DagmedyaVeri">@DagmedyaVeri</a>        |   1.129|
|   449| <a href="https://twitter.com/zuckerco">@zuckerco</a>                |   1.129|
|   450| <a href="https://twitter.com/RobertMaguire_">@RobertMaguire\_</a>   |   1.129|
|   451| <a href="https://twitter.com/realavivahr">@realavivahr</a>          |   1.129|
|   452| <a href="https://twitter.com/portlandmercury">@portlandmercury</a>  |   1.129|
|   453| <a href="https://twitter.com/kcecireyes">@kcecireyes</a>            |   1.129|
|   454| <a href="https://twitter.com/abraji">@abraji</a>                    |   1.129|
|   455| <a href="https://twitter.com/RobertBenincasa">@RobertBenincasa</a>  |   1.129|
|   456| <a href="https://twitter.com/DATABASE_HULK">@DATABASE\_HULK</a>     |   1.129|
|   457| <a href="https://twitter.com/BBGVisualData">@BBGVisualData</a>      |   1.129|
|   458| <a href="https://twitter.com/zammagazine">@zammagazine</a>          |   1.129|
|   459| <a href="https://twitter.com/jczamora">@jczamora</a>                |   1.129|
|   460| <a href="https://twitter.com/StefanieMurray">@StefanieMurray</a>    |   1.129|
|   461| <a href="https://twitter.com/_chloelessard_">@\_chloelessard\_</a>  |   0.944|
|   462| <a href="https://twitter.com/ZapOracles">@ZapOracles</a>            |   0.944|
|   463| <a href="https://twitter.com/MeganLuther">@MeganLuther</a>          |   0.944|
|   464| <a href="https://twitter.com/bethfertig">@bethfertig</a>            |   0.944|
|   465| <a href="https://twitter.com/MattCData">@MattCData</a>              |   0.944|
|   466| <a href="https://twitter.com/kissane">@kissane</a>                  |   0.944|
|   467| <a href="https://twitter.com/wwrfd">@wwrfd</a>                      |   0.702|
|   468| <a href="https://twitter.com/gteresa">@gteresa</a>                  |   0.702|
|   469| <a href="https://twitter.com/kvnmiller">@kvnmiller</a>              |   0.702|
|   470| <a href="https://twitter.com/mcarmichael">@mcarmichael</a>          |   0.702|
|   471| <a href="https://twitter.com/aweiss">@aweiss</a>                    |   0.702|
|   472| <a href="https://twitter.com/davidbschultz">@davidbschultz</a>      |   0.702|
|   473| <a href="https://twitter.com/tkb">@tkb</a>                          |   0.702|
|   474| <a href="https://twitter.com/Brizzyc">@Brizzyc</a>                  |   0.702|
|   475| <a href="https://twitter.com/GerryLanosga">@GerryLanosga</a>        |   0.702|
|   476| <a href="https://twitter.com/Bahareh360">@Bahareh360</a>            |   0.702|
|   477| <a href="https://twitter.com/asincopado">@asincopado</a>            |   0.702|
|   478| <a href="https://twitter.com/The_Dean">@The\_Dean</a>               |   0.702|
|   479| <a href="https://twitter.com/liladerm">@liladerm</a>                |   0.333|
|   480| <a href="https://twitter.com/davelevinthal">@davelevinthal</a>      |   0.333|
|   481| <a href="https://twitter.com/gijnArabic">@gijnArabic</a>            |   0.333|
|   482| <a href="https://twitter.com/DanJFord">@DanJFord</a>                |   0.333|
|   483| <a href="https://twitter.com/joemfox">@joemfox</a>                  |   0.333|
|   484| <a href="https://twitter.com/MMInvestigates">@MMInvestigates</a>    |   0.333|
|   485| <a href="https://twitter.com/NCDJ_ASU">@NCDJ\_ASU</a>               |   0.333|
|   486| <a href="https://twitter.com/rdmurphy">@rdmurphy</a>                |   0.333|
|   487| <a href="https://twitter.com/noeL_maS">@noeL\_maS</a>               |   0.333|
|   488| <a href="https://twitter.com/mediatwit">@mediatwit</a>              |   0.333|
|   489| <a href="https://twitter.com/MediaShiftOrg">@MediaShiftOrg</a>      |   0.333|
|   490| <a href="https://twitter.com/FrancescaFionda">@FrancescaFionda</a>  |   0.333|
