---
title       : Visualising alcohol-related hospital admissions in English local authorities
subtitle    : Created for the 'developing data products' Coursera
author      : Steven Senior
job         : 
framework   : io2012      	# {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  	# {highlight.js, prettify, highlight}
hitheme     : tomorrow      	# 
widgets     : [shiny, interactive, bootstrap]   # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

<style>
.title-slide {
  background-color: #FFFFFF; /* #EDE0CF; ; #CA9F9D*/
}

.title-slide hgroup > h1{
 font-family: 'Baskerville', 'Times', serif; 
 font-weight: light;
}

.title-slide hgroup > h1, 
.title-slide hgroup > h2 {
  font-family: 'Baskerville';
  font-weight: normal;
  color: #535E43 ;  /* ; #EF5150*/
}

article p, article li, article li.build, section p, section li{
  font-family: 'Baskerville','Crimson Text', 'Garamond',  'Palatino', sans-serif;
  text-align: justify;
  font-size:22px;
  line-height: 1.5em;
  color: #444;
}

slide:not(.segue) h2{
  font-family: 'Baskerville', Arial, sans-serif;
  font-size: 52px;
  font-style: normal;
  font-weight: normal;
  text-transform: normal;
  letter-spacing: -2px;
  line-height: 1.2em;
/*  color: #193441;*/
/*  color: #02574D;*/
  color: #333333;
}
</style>

## Available is not the same as accessible

* In the past few years there has been a push to make government data open and available on the web. Following the US lead, the UK Government created data.gov.uk. There is now a wealth of data relevant to public policy available there.

* But just because the data is on the web, doesn't make it accessible to the public. Most people don't spend a lot of time poking around dry spreadsheets on government websites. There is a need for simple, engaging visualisations of this data to draw attention to it and to make it more meaningful for the public.

* As a proof-of-concept, I have chosen to look at alcohol-related hospital admissions. Misuse of alcohol creates a big burden on the health care system in the UK and elsewhere. Alcohol misuse accounted for over 21,000 deaths in the UK in 2012. It is linked to heart disease, stroke, liver disease and cancer. Alcohol is involved in around half of violent crime and contributes to a significant proportion of accident and emergency admissions.

* Better visualisations of this impact might help to focus attention on the problem.

--- .class #id 

## Project outline

There is some evidence that showing people how they compare to their neighbours can improve behaviours like energy use. The aim here is to do the same thing at the local authority level, nudging those with the biggest problem to do something about it.

Alcohol health data is taken from [www.data.gov.uk](http://www.data.gov.uk). This data is *not* tidy. I've written some code to download it and tidy it up.

A density plot shows the distribution of alcohol-related hospital admissions. A vertical line shows where a given local authority is and the shaded the area shows how many local authorities had lower (i.e. better) alcohol-related hospital admissions per 100,000 residents. The next slide shows what this looks like.

Finally, I've turned this into a Shiny app. The app allows the user to select which area and gender they'd like to view data for using two input widgets. The app then shows where that local authority sits in the distribution of local authorities. It also calculates what percentage of local authorities had better statistics.

--- .class #id

## Demo

<div class="row-fluid">
  <div class="col-sm-4">
    <form class="well">
      <div class="form-group shiny-input-container">
        <label class="control-label" for="la">Local authority:</label>
        <div>
          <select id="la"><option value="County Durham" selected>County Durham</option>
<option value="Darlington">Darlington</option>
<option value="Gateshead">Gateshead</option>
<option value="Hartlepool">Hartlepool</option>
<option value="Middlesbrough">Middlesbrough</option>
<option value="Newcastle upon Tyne">Newcastle upon Tyne</option>
<option value="North Tyneside">North Tyneside</option>
<option value="Northumberland">Northumberland</option>
<option value="Redcar and Cleveland">Redcar and Cleveland</option>
<option value="South Tyneside">South Tyneside</option>
<option value="Stockton-on-Tees">Stockton-on-Tees</option>
<option value="Sunderland">Sunderland</option>
<option value="Blackburn with Darwen">Blackburn with Darwen</option>
<option value="Blackpool">Blackpool</option>
<option value="Bolton">Bolton</option>
<option value="Bury">Bury</option>
<option value="Cheshire East">Cheshire East</option>
<option value="Cheshire West and Chester">Cheshire West and Chester</option>
<option value="Cumbria">Cumbria</option>
<option value="Allerdale">Allerdale</option>
<option value="Barrow-in-Furness">Barrow-in-Furness</option>
<option value="Carlisle">Carlisle</option>
<option value="Copeland">Copeland</option>
<option value="Eden">Eden</option>
<option value="South Lakeland">South Lakeland</option>
<option value="Halton">Halton</option>
<option value="Knowsley">Knowsley</option>
<option value="Liverpool">Liverpool</option>
<option value="Lancashire">Lancashire</option>
<option value="Burnley">Burnley</option>
<option value="Chorley">Chorley</option>
<option value="Fylde">Fylde</option>
<option value="Hyndburn">Hyndburn</option>
<option value="Lancaster">Lancaster</option>
<option value="Pendle">Pendle</option>
<option value="Preston">Preston</option>
<option value="Ribble Valley">Ribble Valley</option>
<option value="Rossendale">Rossendale</option>
<option value="South Ribble">South Ribble</option>
<option value="West Lancashire">West Lancashire</option>
<option value="Wyre">Wyre</option>
<option value="Manchester">Manchester</option>
<option value="Oldham">Oldham</option>
<option value="Rochdale">Rochdale</option>
<option value="Salford">Salford</option>
<option value="Sefton">Sefton</option>
<option value="St. Helens">St. Helens</option>
<option value="Stockport">Stockport</option>
<option value="Tameside">Tameside</option>
<option value="Trafford">Trafford</option>
<option value="Warrington">Warrington</option>
<option value="Wigan">Wigan</option>
<option value="Wirral">Wirral</option>
<option value="Barnsley">Barnsley</option>
<option value="Bradford">Bradford</option>
<option value="Calderdale">Calderdale</option>
<option value="Doncaster">Doncaster</option>
<option value="East Riding of Yorkshire">East Riding of Yorkshire</option>
<option value="Kingston upon Hull, City of">Kingston upon Hull, City of</option>
<option value="Kirklees">Kirklees</option>
<option value="Leeds">Leeds</option>
<option value="North East Lincolnshire">North East Lincolnshire</option>
<option value="North Lincolnshire">North Lincolnshire</option>
<option value="North Yorkshire">North Yorkshire</option>
<option value="Craven">Craven</option>
<option value="Hambleton">Hambleton</option>
<option value="Harrogate">Harrogate</option>
<option value="Richmondshire">Richmondshire</option>
<option value="Ryedale">Ryedale</option>
<option value="Scarborough">Scarborough</option>
<option value="Selby">Selby</option>
<option value="Rotherham">Rotherham</option>
<option value="Sheffield">Sheffield</option>
<option value="Wakefield">Wakefield</option>
<option value="York">York</option>
<option value="Derby">Derby</option>
<option value="Derbyshire">Derbyshire</option>
<option value="Amber Valley">Amber Valley</option>
<option value="Bolsover">Bolsover</option>
<option value="Chesterfield">Chesterfield</option>
<option value="Derbyshire Dales">Derbyshire Dales</option>
<option value="Erewash">Erewash</option>
<option value="High Peak">High Peak</option>
<option value="North East Derbyshire">North East Derbyshire</option>
<option value="South Derbyshire">South Derbyshire</option>
<option value="Leicester">Leicester</option>
<option value="Leicestershire">Leicestershire</option>
<option value="Blaby">Blaby</option>
<option value="Charnwood">Charnwood</option>
<option value="Harborough">Harborough</option>
<option value="Hinckley and Bosworth">Hinckley and Bosworth</option>
<option value="Melton">Melton</option>
<option value="North West Leicestershire">North West Leicestershire</option>
<option value="Oadby and Wigston">Oadby and Wigston</option>
<option value="Lincolnshire">Lincolnshire</option>
<option value="Boston">Boston</option>
<option value="East Lindsey">East Lindsey</option>
<option value="Lincoln">Lincoln</option>
<option value="North Kesteven">North Kesteven</option>
<option value="South Holland">South Holland</option>
<option value="South Kesteven">South Kesteven</option>
<option value="West Lindsey">West Lindsey</option>
<option value="Northamptonshire">Northamptonshire</option>
<option value="Corby">Corby</option>
<option value="Daventry">Daventry</option>
<option value="East Northamptonshire">East Northamptonshire</option>
<option value="Kettering">Kettering</option>
<option value="Northampton">Northampton</option>
<option value="South Northamptonshire">South Northamptonshire</option>
<option value="Wellingborough">Wellingborough</option>
<option value="Nottingham">Nottingham</option>
<option value="Nottinghamshire">Nottinghamshire</option>
<option value="Ashfield">Ashfield</option>
<option value="Bassetlaw">Bassetlaw</option>
<option value="Broxtowe">Broxtowe</option>
<option value="Gedling">Gedling</option>
<option value="Mansfield">Mansfield</option>
<option value="Newark and Sherwood">Newark and Sherwood</option>
<option value="Rushcliffe">Rushcliffe</option>
<option value="Rutland">Rutland</option>
<option value="Birmingham">Birmingham</option>
<option value="Coventry">Coventry</option>
<option value="Dudley">Dudley</option>
<option value="Herefordshire, County of">Herefordshire, County of</option>
<option value="Sandwell">Sandwell</option>
<option value="Shropshire">Shropshire</option>
<option value="Solihull">Solihull</option>
<option value="Staffordshire">Staffordshire</option>
<option value="Cannock Chase">Cannock Chase</option>
<option value="East Staffordshire">East Staffordshire</option>
<option value="Lichfield">Lichfield</option>
<option value="Newcastle-under-Lyme">Newcastle-under-Lyme</option>
<option value="South Staffordshire">South Staffordshire</option>
<option value="Stafford">Stafford</option>
<option value="Staffordshire Moorlands">Staffordshire Moorlands</option>
<option value="Tamworth">Tamworth</option>
<option value="Stoke-on-Trent">Stoke-on-Trent</option>
<option value="Telford and Wrekin">Telford and Wrekin</option>
<option value="Walsall">Walsall</option>
<option value="Warwickshire">Warwickshire</option>
<option value="North Warwickshire">North Warwickshire</option>
<option value="Nuneaton and Bedworth">Nuneaton and Bedworth</option>
<option value="Rugby">Rugby</option>
<option value="Stratford-on-Avon">Stratford-on-Avon</option>
<option value="Warwick">Warwick</option>
<option value="Wolverhampton">Wolverhampton</option>
<option value="Worcestershire">Worcestershire</option>
<option value="Bromsgrove">Bromsgrove</option>
<option value="Malvern Hills">Malvern Hills</option>
<option value="Redditch">Redditch</option>
<option value="Worcester">Worcester</option>
<option value="Wychavon">Wychavon</option>
<option value="Wyre Forest">Wyre Forest</option>
<option value="Bedford">Bedford</option>
<option value="Cambridgeshire">Cambridgeshire</option>
<option value="Cambridge">Cambridge</option>
<option value="East Cambridgeshire">East Cambridgeshire</option>
<option value="Fenland">Fenland</option>
<option value="Huntingdonshire">Huntingdonshire</option>
<option value="South Cambridgeshire">South Cambridgeshire</option>
<option value="Central Bedfordshire">Central Bedfordshire</option>
<option value="Essex">Essex</option>
<option value="Basildon">Basildon</option>
<option value="Braintree">Braintree</option>
<option value="Brentwood">Brentwood</option>
<option value="Castle Point">Castle Point</option>
<option value="Chelmsford">Chelmsford</option>
<option value="Colchester">Colchester</option>
<option value="Epping Forest">Epping Forest</option>
<option value="Harlow">Harlow</option>
<option value="Maldon">Maldon</option>
<option value="Rochford">Rochford</option>
<option value="Tendring">Tendring</option>
<option value="Uttlesford">Uttlesford</option>
<option value="Hertfordshire">Hertfordshire</option>
<option value="Broxbourne">Broxbourne</option>
<option value="Dacorum">Dacorum</option>
<option value="East Hertfordshire">East Hertfordshire</option>
<option value="Hertsmere">Hertsmere</option>
<option value="North Hertfordshire">North Hertfordshire</option>
<option value="St. Albans">St. Albans</option>
<option value="Stevenage">Stevenage</option>
<option value="Three Rivers">Three Rivers</option>
<option value="Watford">Watford</option>
<option value="Welwyn Hatfield">Welwyn Hatfield</option>
<option value="Luton">Luton</option>
<option value="Norfolk">Norfolk</option>
<option value="Breckland">Breckland</option>
<option value="Broadland">Broadland</option>
<option value="Great Yarmouth">Great Yarmouth</option>
<option value="King's Lynn and West Norfolk">King's Lynn and West Norfolk</option>
<option value="North Norfolk">North Norfolk</option>
<option value="Norwich">Norwich</option>
<option value="South Norfolk">South Norfolk</option>
<option value="Peterborough">Peterborough</option>
<option value="Southend-on-Sea">Southend-on-Sea</option>
<option value="Suffolk">Suffolk</option>
<option value="Babergh">Babergh</option>
<option value="Forest Heath">Forest Heath</option>
<option value="Ipswich">Ipswich</option>
<option value="Mid Suffolk">Mid Suffolk</option>
<option value="St. Edmundsbury">St. Edmundsbury</option>
<option value="Suffolk Coastal">Suffolk Coastal</option>
<option value="Waveney">Waveney</option>
<option value="Thurrock">Thurrock</option>
<option value="City of London">City of London</option>
<option value="Barking and Dagenham">Barking and Dagenham</option>
<option value="Barnet">Barnet</option>
<option value="Bexley">Bexley</option>
<option value="Brent">Brent</option>
<option value="Bromley">Bromley</option>
<option value="Camden">Camden</option>
<option value="Croydon">Croydon</option>
<option value="Ealing">Ealing</option>
<option value="Enfield">Enfield</option>
<option value="Greenwich">Greenwich</option>
<option value="Hackney">Hackney</option>
<option value="Hammersmith and Fulham">Hammersmith and Fulham</option>
<option value="Haringey">Haringey</option>
<option value="Harrow">Harrow</option>
<option value="Havering">Havering</option>
<option value="Hillingdon">Hillingdon</option>
<option value="Hounslow">Hounslow</option>
<option value="Islington">Islington</option>
<option value="Kensington and Chelsea">Kensington and Chelsea</option>
<option value="Kingston upon Thames">Kingston upon Thames</option>
<option value="Lambeth">Lambeth</option>
<option value="Lewisham">Lewisham</option>
<option value="Merton">Merton</option>
<option value="Newham">Newham</option>
<option value="Redbridge">Redbridge</option>
<option value="Richmond upon Thames">Richmond upon Thames</option>
<option value="Southwark">Southwark</option>
<option value="Sutton">Sutton</option>
<option value="Tower Hamlets">Tower Hamlets</option>
<option value="Waltham Forest">Waltham Forest</option>
<option value="Wandsworth">Wandsworth</option>
<option value="Westminster">Westminster</option>
<option value="Bracknell Forest">Bracknell Forest</option>
<option value="Brighton and Hove">Brighton and Hove</option>
<option value="Buckinghamshire">Buckinghamshire</option>
<option value="Aylesbury Vale">Aylesbury Vale</option>
<option value="Chiltern">Chiltern</option>
<option value="South Bucks">South Bucks</option>
<option value="Wycombe">Wycombe</option>
<option value="East Sussex">East Sussex</option>
<option value="Eastbourne">Eastbourne</option>
<option value="Hastings">Hastings</option>
<option value="Lewes">Lewes</option>
<option value="Rother">Rother</option>
<option value="Wealden">Wealden</option>
<option value="Hampshire">Hampshire</option>
<option value="Basingstoke and Deane">Basingstoke and Deane</option>
<option value="East Hampshire">East Hampshire</option>
<option value="Eastleigh">Eastleigh</option>
<option value="Fareham">Fareham</option>
<option value="Gosport">Gosport</option>
<option value="Hart">Hart</option>
<option value="Havant">Havant</option>
<option value="New Forest">New Forest</option>
<option value="Rushmoor">Rushmoor</option>
<option value="Test Valley">Test Valley</option>
<option value="Winchester">Winchester</option>
<option value="Isle of Wight">Isle of Wight</option>
<option value="Kent">Kent</option>
<option value="Ashford">Ashford</option>
<option value="Canterbury">Canterbury</option>
<option value="Dartford">Dartford</option>
<option value="Dover">Dover</option>
<option value="Gravesham">Gravesham</option>
<option value="Maidstone">Maidstone</option>
<option value="Sevenoaks">Sevenoaks</option>
<option value="Shepway">Shepway</option>
<option value="Swale">Swale</option>
<option value="Thanet">Thanet</option>
<option value="Tonbridge and Malling">Tonbridge and Malling</option>
<option value="Tunbridge Wells">Tunbridge Wells</option>
<option value="Medway">Medway</option>
<option value="Milton Keynes">Milton Keynes</option>
<option value="Oxfordshire">Oxfordshire</option>
<option value="Cherwell">Cherwell</option>
<option value="Oxford">Oxford</option>
<option value="South Oxfordshire">South Oxfordshire</option>
<option value="Vale of White Horse">Vale of White Horse</option>
<option value="West Oxfordshire">West Oxfordshire</option>
<option value="Portsmouth">Portsmouth</option>
<option value="Reading">Reading</option>
<option value="Slough">Slough</option>
<option value="Southampton">Southampton</option>
<option value="Surrey">Surrey</option>
<option value="Elmbridge">Elmbridge</option>
<option value="Epsom and Ewell">Epsom and Ewell</option>
<option value="Guildford">Guildford</option>
<option value="Mole Valley">Mole Valley</option>
<option value="Reigate and Banstead">Reigate and Banstead</option>
<option value="Runnymede">Runnymede</option>
<option value="Spelthorne">Spelthorne</option>
<option value="Surrey Heath">Surrey Heath</option>
<option value="Tandridge">Tandridge</option>
<option value="Waverley">Waverley</option>
<option value="Woking">Woking</option>
<option value="West Berkshire">West Berkshire</option>
<option value="West Sussex">West Sussex</option>
<option value="Adur">Adur</option>
<option value="Arun">Arun</option>
<option value="Chichester">Chichester</option>
<option value="Crawley">Crawley</option>
<option value="Horsham">Horsham</option>
<option value="Mid Sussex">Mid Sussex</option>
<option value="Worthing">Worthing</option>
<option value="Windsor and Maidenhead">Windsor and Maidenhead</option>
<option value="Wokingham">Wokingham</option>
<option value="Bath and North East Somerset">Bath and North East Somerset</option>
<option value="Bournemouth">Bournemouth</option>
<option value="Bristol, City of">Bristol, City of</option>
<option value="Cornwall">Cornwall</option>
<option value="Isles of Scilly">Isles of Scilly</option>
<option value="Devon">Devon</option>
<option value="East Devon">East Devon</option>
<option value="Exeter">Exeter</option>
<option value="Mid Devon">Mid Devon</option>
<option value="North Devon">North Devon</option>
<option value="South Hams">South Hams</option>
<option value="Teignbridge">Teignbridge</option>
<option value="Torridge">Torridge</option>
<option value="West Devon">West Devon</option>
<option value="Dorset">Dorset</option>
<option value="Christchurch">Christchurch</option>
<option value="East Dorset">East Dorset</option>
<option value="North Dorset">North Dorset</option>
<option value="Purbeck">Purbeck</option>
<option value="West Dorset">West Dorset</option>
<option value="Weymouth and Portland">Weymouth and Portland</option>
<option value="Gloucestershire">Gloucestershire</option>
<option value="Cheltenham">Cheltenham</option>
<option value="Cotswold">Cotswold</option>
<option value="Forest of Dean">Forest of Dean</option>
<option value="Gloucester">Gloucester</option>
<option value="Stroud">Stroud</option>
<option value="Tewkesbury">Tewkesbury</option>
<option value="North Somerset">North Somerset</option>
<option value="Plymouth">Plymouth</option>
<option value="Poole">Poole</option>
<option value="Somerset">Somerset</option>
<option value="Mendip">Mendip</option>
<option value="Sedgemoor">Sedgemoor</option>
<option value="South Somerset">South Somerset</option>
<option value="Taunton Deane">Taunton Deane</option>
<option value="West Somerset">West Somerset</option>
<option value="South Gloucestershire">South Gloucestershire</option>
<option value="Swindon">Swindon</option>
<option value="Torbay">Torbay</option>
<option value="Wiltshire">Wiltshire</option></select>
          <script type="application/json" data-for="la" data-nonempty="">{}</script>
        </div>
      </div>
      <div class="form-group shiny-input-container">
        <label class="control-label" for="sex">Choose sex to view data for:</label>
        <div>
          <select id="sex"><option value="both" selected>both</option>
<option value="female">female</option>
<option value="male">male</option></select>
          <script type="application/json" data-for="sex" data-nonempty="">{}</script>
        </div>
      </div>
    </form>
  </div>
  <div class="col-sm-8">
    <div id="myPlot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
    <h3>Summary of output:</h3>
    <h4>Local Authority:</h4>
    <pre id="Text1" class="shiny-text-output"></pre>
    <h4>Alcohol-related hospital admissions per 100,000 people:</h4>
    <pre id="Text2" class="shiny-text-output"></pre>
    <h4>% of local authorities that are better than your area:</h4>
    <pre id="Text3" class="shiny-text-output"></pre>
  </div>
</div>

--- .class #id

## So who cares?

Some examples of people who could be interested in this sort of data include:

1. Local politicians, local government officials
2. Local public health practitioners and health providers
3. People looking to move to a new area
4. Concerned residents!

## So what next?

I plan to keep building interactive visualisations of open government data. This will build up a library of apps that users could browse by category. Hopefully this will go a small way to making this data more accessible.

Thanks for reading!


