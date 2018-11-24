
__Meeting 11/20/2018 Joanna Wang, Douglas Xu__


```R
library(car)
```

    Loading required package: carData
    


```R
data <- read.csv(file="crime_v2.csv", header=TRUE, sep=",",na.strings=c("`","","NA"))
```


```R
objects(data)
```


<ol class=list-inline>
	<li>'avgsen'</li>
	<li>'central'</li>
	<li>'county'</li>
	<li>'crmrte'</li>
	<li>'density'</li>
	<li>'mix'</li>
	<li>'pctmin80'</li>
	<li>'pctymle'</li>
	<li>'polpc'</li>
	<li>'prbarr'</li>
	<li>'prbconv'</li>
	<li>'prbpris'</li>
	<li>'taxpc'</li>
	<li>'urban'</li>
	<li>'wcon'</li>
	<li>'west'</li>
	<li>'wfed'</li>
	<li>'wfir'</li>
	<li>'wloc'</li>
	<li>'wmfg'</li>
	<li>'wser'</li>
	<li>'wsta'</li>
	<li>'wtrd'</li>
	<li>'wtuc'</li>
	<li>'year'</li>
</ol>




```R
summary(data)
```


         county           year        crmrte             prbarr       
     Min.   :  1.0   Min.   :87   Min.   :0.005533   Min.   :0.09277  
     1st Qu.: 52.0   1st Qu.:87   1st Qu.:0.020927   1st Qu.:0.20568  
     Median :105.0   Median :87   Median :0.029986   Median :0.27095  
     Mean   :101.6   Mean   :87   Mean   :0.033400   Mean   :0.29492  
     3rd Qu.:152.0   3rd Qu.:87   3rd Qu.:0.039642   3rd Qu.:0.34438  
     Max.   :197.0   Max.   :87   Max.   :0.098966   Max.   :1.09091  
     NA's   :6       NA's   :6    NA's   :6          NA's   :6        
        prbconv           prbpris           avgsen           polpc         
     Min.   :0.06838   Min.   :0.1500   Min.   : 5.380   Min.   :0.000746  
     1st Qu.:0.34541   1st Qu.:0.3648   1st Qu.: 7.340   1st Qu.:0.001231  
     Median :0.45283   Median :0.4234   Median : 9.100   Median :0.001485  
     Mean   :0.55128   Mean   :0.4108   Mean   : 9.647   Mean   :0.001702  
     3rd Qu.:0.58886   3rd Qu.:0.4568   3rd Qu.:11.420   3rd Qu.:0.001877  
     Max.   :2.12121   Max.   :0.6000   Max.   :20.700   Max.   :0.009054  
     NA's   :6         NA's   :6        NA's   :6        NA's   :6         
        density            taxpc             west           central      
     Min.   :0.00002   Min.   : 25.69   Min.   :0.0000   Min.   :0.0000  
     1st Qu.:0.54741   1st Qu.: 30.66   1st Qu.:0.0000   1st Qu.:0.0000  
     Median :0.96226   Median : 34.87   Median :0.0000   Median :0.0000  
     Mean   :1.42884   Mean   : 38.06   Mean   :0.2527   Mean   :0.3736  
     3rd Qu.:1.56824   3rd Qu.: 40.95   3rd Qu.:0.5000   3rd Qu.:1.0000  
     Max.   :8.82765   Max.   :119.76   Max.   :1.0000   Max.   :1.0000  
     NA's   :6         NA's   :6        NA's   :6        NA's   :6       
         urban            pctmin80           wcon            wtuc      
     Min.   :0.00000   Min.   : 1.284   Min.   :193.6   Min.   :187.6  
     1st Qu.:0.00000   1st Qu.: 9.845   1st Qu.:250.8   1st Qu.:374.6  
     Median :0.00000   Median :24.312   Median :281.4   Median :406.5  
     Mean   :0.08791   Mean   :25.495   Mean   :285.4   Mean   :411.7  
     3rd Qu.:0.00000   3rd Qu.:38.142   3rd Qu.:314.8   3rd Qu.:443.4  
     Max.   :1.00000   Max.   :64.348   Max.   :436.8   Max.   :613.2  
     NA's   :6         NA's   :6        NA's   :6       NA's   :6      
          wtrd            wfir            wser             wmfg      
     Min.   :154.2   Min.   :170.9   Min.   : 133.0   Min.   :157.4  
     1st Qu.:190.9   1st Qu.:286.5   1st Qu.: 229.7   1st Qu.:288.9  
     Median :203.0   Median :317.3   Median : 253.2   Median :320.2  
     Mean   :211.6   Mean   :322.1   Mean   : 275.6   Mean   :335.6  
     3rd Qu.:225.1   3rd Qu.:345.4   3rd Qu.: 280.5   3rd Qu.:359.6  
     Max.   :354.7   Max.   :509.5   Max.   :2177.1   Max.   :646.9  
     NA's   :6       NA's   :6       NA's   :6        NA's   :6      
          wfed            wsta            wloc            mix         
     Min.   :326.1   Min.   :258.3   Min.   :239.2   Min.   :0.01961  
     1st Qu.:400.2   1st Qu.:329.3   1st Qu.:297.3   1st Qu.:0.08074  
     Median :449.8   Median :357.7   Median :308.1   Median :0.10186  
     Mean   :442.9   Mean   :357.5   Mean   :312.7   Mean   :0.12884  
     3rd Qu.:478.0   3rd Qu.:382.6   3rd Qu.:329.2   3rd Qu.:0.15175  
     Max.   :598.0   Max.   :499.6   Max.   :388.1   Max.   :0.46512  
     NA's   :6       NA's   :6       NA's   :6       NA's   :6        
        pctymle       
     Min.   :0.06216  
     1st Qu.:0.07443  
     Median :0.07771  
     Mean   :0.08396  
     3rd Qu.:0.08350  
     Max.   :0.24871  
     NA's   :6        


1. 6 NA
2. take out year column
3. "prbarr" max > 1
4. "prbconv" strange characters and blank spaces; also the probability is bigger than 1
5. taxpc, what is the unit, what does it mean? Outlier at 119. Is the unit %?
6. pctmin80 data is too old
7. 15-23: different industry avg. wages
8. 24 mix: ratio of face-to-face crime
9. percentage young male (what is the age:15-24)

Plan before Thrusday:
1. research question
2. identify the relevant variables


```R
tail(data,50)
hist(data$prbconv)
```


<table>
<thead><tr><th></th><th scope=col>county</th><th scope=col>year</th><th scope=col>crmrte</th><th scope=col>prbarr</th><th scope=col>prbconv</th><th scope=col>prbpris</th><th scope=col>avgsen</th><th scope=col>polpc</th><th scope=col>density</th><th scope=col>taxpc</th><th scope=col>...</th><th scope=col>wtuc</th><th scope=col>wtrd</th><th scope=col>wfir</th><th scope=col>wser</th><th scope=col>wmfg</th><th scope=col>wfed</th><th scope=col>wsta</th><th scope=col>wloc</th><th scope=col>mix</th><th scope=col>pctymle</th></tr></thead>
<tbody>
	<tr><th scope=row>48</th><td>109         </td><td>87          </td><td>0.0230995   </td><td>0.162769    </td><td>0.781609    </td><td>0.411765    </td><td> 9.12       </td><td>0.00108043  </td><td>1.5939596890</td><td>27.32160    </td><td>...         </td><td>374.0296    </td><td>226.4881    </td><td>335.4204    </td><td> 230.3086   </td><td>320.20      </td><td>453.61      </td><td>389.34      </td><td>302.93      </td><td>0.05424063  </td><td>0.08050946  </td></tr>
	<tr><th scope=row>49</th><td>111         </td><td>87          </td><td>0.0183048   </td><td>0.202112    </td><td>0.522388    </td><td>0.542857    </td><td>11.06       </td><td>0.00118719  </td><td>0.8306636210</td><td>29.58239    </td><td>...         </td><td>571.5438    </td><td>179.5039    </td><td>327.9666    </td><td> 251.4270   </td><td>260.35      </td><td>384.15      </td><td>354.41      </td><td>304.91      </td><td>0.06763285  </td><td>0.06861899  </td></tr>
	<tr><th scope=row>50</th><td>113         </td><td>87          </td><td>0.0142071   </td><td>0.179878    </td><td>0.220339    </td><td>0.461538    </td><td> 6.39       </td><td>0.00151600  </td><td>0.4487427470</td><td>40.80142    </td><td>...         </td><td>412.0879    </td><td>154.2090    </td><td>256.4102    </td><td> 265.1301   </td><td>291.10      </td><td>337.09      </td><td>374.11      </td><td>246.65      </td><td>0.05128205  </td><td>0.09171820  </td></tr>
	<tr><th scope=row>51</th><td>115         </td><td>87          </td><td>0.0055332   </td><td>1.090910    </td><td>1.500000    </td><td>0.500000    </td><td>20.70       </td><td>0.00905433  </td><td>0.3858093020</td><td>28.19310    </td><td>...         </td><td>503.2351    </td><td>217.4908    </td><td>342.4658    </td><td> 245.2061   </td><td>448.42      </td><td>442.20      </td><td>340.39      </td><td>386.12      </td><td>0.10000000  </td><td>0.07253495  </td></tr>
	<tr><th scope=row>52</th><td>117         </td><td>87          </td><td>0.0268723   </td><td>0.370474    </td><td>0.793233    </td><td>0.236967    </td><td>11.83       </td><td>0.00119765  </td><td>0.5813449030</td><td>38.81493    </td><td>...         </td><td>424.7286    </td><td>167.0511    </td><td>282.4099    </td><td> 229.0151   </td><td>327.29      </td><td>383.88      </td><td>360.66      </td><td>302.03      </td><td>0.07485030  </td><td>0.07632116  </td></tr>
	<tr><th scope=row>53</th><td>119         </td><td>87          </td><td>0.0989659   </td><td>0.149094    </td><td>0.347800    </td><td>0.486183    </td><td> 7.13       </td><td>0.00223135  </td><td>8.8276519780</td><td>75.67243    </td><td>...         </td><td>548.3239    </td><td>354.6761    </td><td>509.4655    </td><td> 354.3007   </td><td>494.30      </td><td>568.40      </td><td>329.22      </td><td>379.77      </td><td>0.16869897  </td><td>0.07916495  </td></tr>
	<tr><th scope=row>54</th><td>123         </td><td>87          </td><td>0.0300184   </td><td>0.487430    </td><td>0.226361    </td><td>0.443038    </td><td> 6.49       </td><td>0.00176086  </td><td>0.4938775600</td><td>38.45734    </td><td>...         </td><td>396.2704    </td><td>193.0723    </td><td>272.2941    </td><td> 242.4605   </td><td>277.34      </td><td>345.09      </td><td>328.00      </td><td>325.77      </td><td>0.31135532  </td><td>0.08119376  </td></tr>
	<tr><th scope=row>55</th><td>125         </td><td>87          </td><td>0.0266287   </td><td>0.269043    </td><td>0.438961    </td><td>0.396450    </td><td> 7.36       </td><td>0.00200971  </td><td>0.8202567700</td><td>48.15414    </td><td>...         </td><td>457.5350    </td><td>199.5847    </td><td>299.7388    </td><td> 320.1325   </td><td>277.68      </td><td>447.87      </td><td>361.24      </td><td>300.77      </td><td>0.07110778  </td><td>0.07415335  </td></tr>
	<tr><th scope=row>56</th><td>127         </td><td>87          </td><td>0.0291496   </td><td>0.179616    </td><td>1.358140    </td><td>0.335616    </td><td>15.99       </td><td>0.00158289  </td><td>1.3388888840</td><td>32.02376    </td><td>...         </td><td>426.3901    </td><td>257.6008    </td><td>441.1413    </td><td> 305.7612   </td><td>329.87      </td><td>508.61      </td><td>380.30      </td><td>329.71      </td><td>0.06305506  </td><td>0.07400288  </td></tr>
	<tr><th scope=row>57</th><td>129         </td><td>87          </td><td>0.0834982   </td><td>0.236601    </td><td>0.393413    </td><td>0.415158    </td><td> 9.57       </td><td>0.00255849  </td><td>6.2864866260</td><td>67.67963    </td><td>...         </td><td>392.0999    </td><td>220.4530    </td><td>363.2880    </td><td> 292.7027   </td><td>464.49      </td><td>548.49      </td><td>421.36      </td><td>319.08      </td><td>0.07871422  </td><td>0.08109921  </td></tr>
	<tr><th scope=row>58</th><td>131         </td><td>87          </td><td>0.0189848   </td><td>0.689024    </td><td>0.495575    </td><td>0.401786    </td><td> 9.97       </td><td>0.00121549  </td><td>0.4126394090</td><td>37.70006    </td><td>...         </td><td>375.2345    </td><td>220.9747    </td><td>307.6923    </td><td> 172.6281   </td><td>278.70      </td><td>432.81      </td><td>370.81      </td><td>259.78      </td><td>0.16725978  </td><td>0.08356434  </td></tr>
	<tr><th scope=row>59</th><td>133         </td><td>87          </td><td>0.0551287   </td><td>0.266960    </td><td>0.271947    </td><td>0.334951    </td><td> 8.99       </td><td>0.00154457  </td><td>1.6500655410</td><td>27.46926    </td><td>...         </td><td>318.9644    </td><td>183.2609    </td><td>265.1232    </td><td> 230.6581   </td><td>258.25      </td><td>326.10      </td><td>329.43      </td><td>301.64      </td><td>0.12176319  </td><td>0.24871162  </td></tr>
	<tr><th scope=row>60</th><td>135         </td><td>87          </td><td>0.0628972   </td><td>0.092770    </td><td>0.477733    </td><td>0.385593    </td><td>11.92       </td><td>0.00233871  </td><td>2.1575000290</td><td>35.99248    </td><td>...         </td><td>420.8830    </td><td>179.1289    </td><td>389.8522    </td><td> 292.2253   </td><td>388.75      </td><td>509.95      </td><td>499.59      </td><td>333.05      </td><td>0.05091770  </td><td>0.13302912  </td></tr>
	<tr><th scope=row>61</th><td>137         </td><td>87          </td><td>0.0126662   </td><td>0.207143    </td><td>1.068970    </td><td>0.322581    </td><td> 6.18       </td><td>0.00081426  </td><td>0.3167155390</td><td>44.29367    </td><td>...         </td><td>356.1254    </td><td>170.8711    </td><td>170.9402    </td><td> 250.8361   </td><td>192.96      </td><td>360.84      </td><td>283.90      </td><td>321.73      </td><td>0.06870229  </td><td>0.07098370  </td></tr>
	<tr><th scope=row>62</th><td>139         </td><td>87          </td><td>0.0243470   </td><td>0.522696    </td><td>0.289474    </td><td>0.345455    </td><td>14.22       </td><td>0.00167448  </td><td>1.3333333730</td><td>29.49915    </td><td>...         </td><td>441.5954    </td><td>201.3569    </td><td>302.6724    </td><td> 260.5459   </td><td>264.25      </td><td>452.59      </td><td>348.05      </td><td>285.47      </td><td>0.34879407  </td><td>0.09625563  </td></tr>
	<tr><th scope=row>63</th><td>141         </td><td>87          </td><td>0.0314610   </td><td>0.238636    </td><td>0.412698    </td><td>0.487179    </td><td>13.18       </td><td>0.00127115  </td><td>0.3005714420</td><td>35.97390    </td><td>...         </td><td>388.3136    </td><td>179.7050    </td><td>263.7363    </td><td> 196.1453   </td><td>255.56      </td><td>374.78      </td><td>380.29      </td><td>294.98      </td><td>0.20000000  </td><td>0.07572646  </td></tr>
	<tr><th scope=row>64</th><td>143         </td><td>87          </td><td>0.0265806   </td><td>0.317857    </td><td>0.314607    </td><td>0.250000    </td><td> 9.36       </td><td>0.00085438  </td><td>0.4349593520</td><td>31.22779    </td><td>...         </td><td>373.9316    </td><td>178.3723    </td><td>234.5216    </td><td> 133.0431   </td><td>157.41      </td><td>380.97      </td><td>388.43      </td><td>253.66      </td><td>0.21212120  </td><td>0.06769374  </td></tr>
	<tr><th scope=row>65</th><td>145         </td><td>87          </td><td>0.0299856   </td><td>0.354733    </td><td>0.340491    </td><td>0.594595    </td><td> 8.47       </td><td>0.00137040  </td><td>0.7788944840</td><td>44.64758    </td><td>...         </td><td>538.8488    </td><td>200.7432    </td><td>302.1978    </td><td> 219.6343   </td><td>334.65      </td><td>414.63      </td><td>298.78      </td><td>295.00      </td><td>0.22533333  </td><td>0.07275662  </td></tr>
	<tr><th scope=row>66</th><td>147         </td><td>87          </td><td>0.0551686   </td><td>0.221542    </td><td>0.426778    </td><td>0.443137    </td><td> 7.73       </td><td>0.00218874  </td><td>1.5159817930</td><td>36.18621    </td><td>...         </td><td>379.8962    </td><td>205.4827    </td><td>377.6978    </td><td> 274.6765   </td><td>390.01      </td><td>543.21      </td><td>464.63      </td><td>330.78      </td><td>0.09345226  </td><td>0.11421655  </td></tr>
	<tr><th scope=row>67</th><td>149         </td><td>87          </td><td>0.0164987   </td><td>0.271967    </td><td>1.015380    </td><td>0.227273    </td><td>14.62       </td><td>0.00151871  </td><td>0.6092436910</td><td>29.03402    </td><td>...         </td><td>437.0629    </td><td>188.7683    </td><td>353.2182    </td><td> 210.4415   </td><td>289.43      </td><td>421.34      </td><td>342.92      </td><td>301.23      </td><td>0.11682243  </td><td>0.06215772  </td></tr>
	<tr><th scope=row>68</th><td>151         </td><td>87          </td><td>0.0264557   </td><td>0.299198    </td><td>0.360153    </td><td>0.340426    </td><td>12.57       </td><td>0.00132430  </td><td>1.2737642530</td><td>25.69287    </td><td>...         </td><td>415.1317    </td><td>218.7198    </td><td>322.4150    </td><td> 278.1124   </td><td>294.37      </td><td>474.26      </td><td>298.66      </td><td>294.72      </td><td>0.07342084  </td><td>0.07763254  </td></tr>
	<tr><th scope=row>69</th><td>153         </td><td>87          </td><td>0.0317563   </td><td>0.345368    </td><td>0.520710    </td><td>0.458333    </td><td>11.33       </td><td>0.00138447  </td><td>0.9622641210</td><td>37.22833    </td><td>...         </td><td>294.6650    </td><td>192.8994    </td><td>267.3797    </td><td> 237.1590   </td><td>301.29      </td><td>467.08      </td><td>350.24      </td><td>302.25      </td><td>0.16323297  </td><td>0.07570874  </td></tr>
	<tr><th scope=row>70</th><td>155         </td><td>87          </td><td>0.0312279   </td><td>0.408200    </td><td>0.559823    </td><td>0.386544    </td><td> 8.71       </td><td>0.00145925  </td><td>1.1296100620</td><td>31.37446    </td><td>...         </td><td>407.0929    </td><td>200.2213    </td><td>337.9095    </td><td> 262.9849   </td><td>278.82      </td><td>441.49      </td><td>381.46      </td><td>304.73      </td><td>0.12516960  </td><td>0.08183564  </td></tr>
	<tr><th scope=row>71</th><td>157         </td><td>87          </td><td>0.0305908   </td><td>0.278287    </td><td>0.443681    </td><td>0.377709    </td><td> 7.48       </td><td>0.00191777  </td><td>1.5096660850</td><td>39.16965    </td><td>...         </td><td>409.7771    </td><td>192.4181    </td><td>302.6162    </td><td> 245.7938   </td><td>418.48      </td><td>478.48      </td><td>342.13      </td><td>318.07      </td><td>0.12467756  </td><td>0.07771273  </td></tr>
	<tr><th scope=row>72</th><td>159         </td><td>87          </td><td>0.0362330   </td><td>0.243590    </td><td>0.492940    </td><td>0.476563    </td><td> 8.64       </td><td>0.00158619  </td><td>2.0192677970</td><td>27.76489    </td><td>...         </td><td>475.3228    </td><td>260.2710    </td><td>329.5464    </td><td> 265.4315   </td><td>374.41      </td><td>491.16      </td><td>346.81      </td><td>351.74      </td><td>0.09146758  </td><td>0.07705218  </td></tr>
	<tr><th scope=row>73</th><td>161         </td><td>87          </td><td>0.0200070   </td><td>0.482425    </td><td>0.508197    </td><td>0.451613    </td><td> 7.98       </td><td>0.00124824  </td><td>1.0052816870</td><td>31.34530    </td><td>...         </td><td>402.5045    </td><td>201.5675    </td><td>279.2492    </td><td> 251.4202   </td><td>334.92      </td><td>450.28      </td><td>277.60      </td><td>302.83      </td><td>0.11024390  </td><td>0.07362188  </td></tr>
	<tr><th scope=row>74</th><td>163         </td><td>87          </td><td>0.0215728   </td><td>0.310987    </td><td>0.401198    </td><td>0.455224    </td><td>11.25       </td><td>0.00136587  </td><td>0.5353748800</td><td>34.01291    </td><td>...         </td><td>415.2824    </td><td>196.5514    </td><td>279.0347    </td><td> 238.6300   </td><td>295.07      </td><td>429.27      </td><td>318.02      </td><td>299.92      </td><td>0.12108560  </td><td>0.07472797  </td></tr>
	<tr><th scope=row>75</th><td>165         </td><td>87          </td><td>0.0508341   </td><td>0.340679    </td><td>0.468531    </td><td>0.432836    </td><td> 7.42       </td><td>0.00151382  </td><td>1.0783698560</td><td>38.74739    </td><td>...         </td><td>471.3424    </td><td>203.0162    </td><td>294.4124    </td><td> 267.6852   </td><td>374.25      </td><td>442.38      </td><td>381.14      </td><td>285.50      </td><td>0.09595300  </td><td>0.08548180  </td></tr>
	<tr><th scope=row>76</th><td>167         </td><td>87          </td><td>0.0238285   </td><td>0.362270    </td><td>0.322581    </td><td>0.371429    </td><td>10.48       </td><td>0.00155144  </td><td>1.2752525810</td><td>35.09686    </td><td>...         </td><td>419.0362    </td><td>221.0995    </td><td>326.8283    </td><td> 253.0096   </td><td>351.09      </td><td>463.69      </td><td>312.53      </td><td>311.47      </td><td>0.10925926  </td><td>0.07687439  </td></tr>
	<tr><th scope=row>77</th><td>169         </td><td>87          </td><td>0.0121033   </td><td>0.343387    </td><td>0.722973    </td><td>0.448598    </td><td>12.36       </td><td>0.00109520  </td><td>0.8008849620</td><td>37.70785    </td><td>...         </td><td>588.6970    </td><td>190.5555    </td><td>331.5650    </td><td> 206.6858   </td><td>306.42      </td><td>406.62      </td><td>348.37      </td><td>306.68      </td><td>0.13720317  </td><td>0.08280677  </td></tr>
	<tr><th scope=row>78</th><td>171         </td><td>87          </td><td>0.0243954   </td><td>0.175649    </td><td>0.909091    </td><td>0.458333    </td><td> 8.67       </td><td>0.00157442  </td><td>1.1521335840</td><td>31.15306    </td><td>...         </td><td>412.5212    </td><td>224.7224    </td><td>339.9547    </td><td> 253.6207   </td><td>288.32      </td><td>452.53      </td><td>341.77      </td><td>324.06      </td><td>0.08207343  </td><td>0.07735254  </td></tr>
	<tr><th scope=row>79</th><td>173         </td><td>87          </td><td>0.0139937   </td><td>0.530435    </td><td>0.327869    </td><td>0.150000    </td><td> 6.64       </td><td>0.00316379  </td><td>0.0000203422</td><td>37.72702    </td><td>...         </td><td>213.6752    </td><td>175.1604    </td><td>267.0940    </td><td> 204.3792   </td><td>193.01      </td><td>334.44      </td><td>414.68      </td><td>304.32      </td><td>0.41975310  </td><td>0.07462687  </td></tr>
	<tr><th scope=row>80</th><td>175         </td><td>87          </td><td>0.0164932   </td><td>0.350348    </td><td>0.410596    </td><td>0.387097    </td><td> 7.31       </td><td>0.00164549  </td><td>0.6878306870</td><td>46.41461    </td><td>...         </td><td>402.5045    </td><td>172.6453    </td><td>317.3394    </td><td> 257.8734   </td><td>627.02      </td><td>344.06      </td><td>357.69      </td><td>298.33      </td><td>0.10230179  </td><td>0.08436658  </td></tr>
	<tr><th scope=row>81</th><td>179         </td><td>87          </td><td>0.0318720   </td><td>0.377543    </td><td>0.328664    </td><td>0.426230    </td><td> 9.90       </td><td>0.00147820  </td><td>1.2816901210</td><td>38.44067    </td><td>...         </td><td>361.1018    </td><td>241.0034    </td><td>342.6819    </td><td> 270.4866   </td><td>349.63      </td><td>459.32      </td><td>387.16      </td><td>376.45      </td><td>0.13481072  </td><td>0.08703093  </td></tr>
	<tr><th scope=row>82</th><td>181         </td><td>87          </td><td>0.0729479   </td><td>0.182590    </td><td>0.343023    </td><td>0.548023    </td><td> 7.06       </td><td>0.00172948  </td><td>1.5702811480</td><td>27.59179    </td><td>...         </td><td>365.4716    </td><td>279.2273    </td><td>325.0271    </td><td> 213.5822   </td><td>290.69      </td><td>453.53      </td><td>317.23      </td><td>286.45      </td><td>0.10003893  </td><td>0.07977433  </td></tr>
	<tr><th scope=row>83</th><td>183         </td><td>87          </td><td>0.0568423   </td><td>0.204216    </td><td>0.381908    </td><td>0.367347    </td><td>12.15       </td><td>0.00212751  </td><td>4.3887586590</td><td>48.76492    </td><td>...         </td><td>528.5593    </td><td>306.0835    </td><td>430.0697    </td><td> 348.2754   </td><td>444.45      </td><td>597.95      </td><td>453.08      </td><td>362.99      </td><td>0.08527010  </td><td>0.09935585  </td></tr>
	<tr><th scope=row>84</th><td>185         </td><td>87          </td><td>0.0108703   </td><td>0.195266    </td><td>2.121210    </td><td>0.442857    </td><td> 5.38       </td><td>0.00122210  </td><td>0.3887587790</td><td>40.82454    </td><td>...         </td><td>331.5650    </td><td>167.3726    </td><td>264.4231    </td><td>2177.0681   </td><td>247.72      </td><td>381.33      </td><td>367.25      </td><td>300.13      </td><td>0.04968944  </td><td>0.07008217  </td></tr>
	<tr><th scope=row>85</th><td>187         </td><td>87          </td><td>0.0345231   </td><td>0.332669    </td><td>0.443114    </td><td>0.432432    </td><td> 6.98       </td><td>0.00116911  </td><td>0.4427710770</td><td>34.71814    </td><td>...         </td><td>421.3483    </td><td>170.5293    </td><td>282.0513    </td><td> 183.1502   </td><td>297.14      </td><td>390.94      </td><td>356.91      </td><td>267.08      </td><td>0.29048842  </td><td>0.07794872  </td></tr>
	<tr><th scope=row>86</th><td>189         </td><td>87          </td><td>0.0313130   </td><td>0.161381    </td><td>0.300578    </td><td>0.288462    </td><td>12.27       </td><td>0.00227837  </td><td>1.1019108300</td><td>31.33022    </td><td>...         </td><td>354.2510    </td><td>180.9359    </td><td>369.4332    </td><td> 253.2281   </td><td>304.72      </td><td>427.84      </td><td>451.79      </td><td>297.19      </td><td>0.05719921  </td><td>0.15092644  </td></tr>
	<tr><th scope=row>87</th><td>191         </td><td>87          </td><td>0.0458895   </td><td>0.172257    </td><td>0.450000    </td><td>0.421053    </td><td> 9.59       </td><td>0.00122733  </td><td>1.7725632190</td><td>32.74533    </td><td>...         </td><td>400.8570    </td><td>230.9888    </td><td>320.0345    </td><td> 238.4958   </td><td>295.26      </td><td>334.55      </td><td>375.45      </td><td>327.62      </td><td>0.08616445  </td><td>0.08828809  </td></tr>
	<tr><th scope=row>88</th><td>193         </td><td>87          </td><td>0.0235277   </td><td>0.266055    </td><td>0.588859    </td><td>0.423423    </td><td> 5.86       </td><td>0.00117887  </td><td>0.8138297800</td><td>28.51783    </td><td>...         </td><td>480.1948    </td><td>268.3836    </td><td>365.0196    </td><td> 295.9352   </td><td>295.63      </td><td>468.26      </td><td>337.88      </td><td>348.74      </td><td>0.11050157  </td><td>0.07819394  </td></tr>
	<tr><th scope=row>89</th><td>193         </td><td>87          </td><td>0.0235277   </td><td>0.266055    </td><td>0.588859    </td><td>0.423423    </td><td> 5.86       </td><td>0.00117887  </td><td>0.8138297800</td><td>28.51783    </td><td>...         </td><td>480.1948    </td><td>268.3836    </td><td>365.0196    </td><td> 295.9352   </td><td>295.63      </td><td>468.26      </td><td>337.88      </td><td>348.74      </td><td>0.11050157  </td><td>0.07819394  </td></tr>
	<tr><th scope=row>90</th><td>195         </td><td>87          </td><td>0.0313973   </td><td>0.201397    </td><td>1.670520    </td><td>0.470588    </td><td>13.02       </td><td>0.00445923  </td><td>1.7459893230</td><td>53.66693    </td><td>...         </td><td>377.9356    </td><td>246.0614    </td><td>411.4330    </td><td> 296.8684   </td><td>392.27      </td><td>480.79      </td><td>303.11      </td><td>337.28      </td><td>0.15612382  </td><td>0.07945071  </td></tr>
	<tr><th scope=row>91</th><td>197         </td><td>87          </td><td>0.0141928   </td><td>0.207595    </td><td>1.182930    </td><td>0.360825    </td><td>12.23       </td><td>0.00118573  </td><td>0.8898809550</td><td>25.95258    </td><td>...         </td><td>341.8803    </td><td>182.8020    </td><td>348.1432    </td><td> 212.8205   </td><td>322.92      </td><td>391.72      </td><td>385.65      </td><td>306.85      </td><td>0.06756757  </td><td>0.07419893  </td></tr>
	<tr><th scope=row>92</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
	<tr><th scope=row>93</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
	<tr><th scope=row>94</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
	<tr><th scope=row>95</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
	<tr><th scope=row>96</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
	<tr><th scope=row>97</th><td> NA         </td><td>NA          </td><td>       NA   </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>   NA       </td><td>        NA  </td><td>          NA</td><td>      NA    </td><td>...         </td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>       NA   </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>    NA      </td><td>        NA  </td><td>        NA  </td></tr>
</tbody>
</table>




![png](output_6_1.png)



```R
scatterplotMatrix(data[3:10])
```


![png](output_7_0.png)



```R
hist(data$taxpc)
```


![png](output_8_0.png)


1. 6 NA
2. take out year column
3. "prbarr" max > 1
4. "prbconv" strange characters and blank spaces; also the probability is bigger than 1
5. taxpc, what is the unit, what does it mean? Outlier at 119. Is the unit %?
6. pctmin80 data is too old
7. 15-23: different industry avg. wages
8. 24 mix: ratio of face-to-face crime
9. percentage young male (what is the age:15-24)

Plan before Thrusday:
1. research question
2. identify the relevant variables

1. remove NA


```R
data <- na.omit(data)
summary(data)
```


         county           year        crmrte             prbarr       
     Min.   :  1.0   Min.   :87   Min.   :0.005533   Min.   :0.09277  
     1st Qu.: 52.0   1st Qu.:87   1st Qu.:0.020927   1st Qu.:0.20568  
     Median :105.0   Median :87   Median :0.029986   Median :0.27095  
     Mean   :101.6   Mean   :87   Mean   :0.033400   Mean   :0.29492  
     3rd Qu.:152.0   3rd Qu.:87   3rd Qu.:0.039642   3rd Qu.:0.34438  
     Max.   :197.0   Max.   :87   Max.   :0.098966   Max.   :1.09091  
        prbconv           prbpris           avgsen           polpc          
     Min.   :0.06838   Min.   :0.1500   Min.   : 5.380   Min.   :0.0007459  
     1st Qu.:0.34541   1st Qu.:0.3648   1st Qu.: 7.340   1st Qu.:0.0012308  
     Median :0.45283   Median :0.4234   Median : 9.100   Median :0.0014853  
     Mean   :0.55128   Mean   :0.4108   Mean   : 9.647   Mean   :0.0017022  
     3rd Qu.:0.58886   3rd Qu.:0.4568   3rd Qu.:11.420   3rd Qu.:0.0018768  
     Max.   :2.12121   Max.   :0.6000   Max.   :20.700   Max.   :0.0090543  
        density            taxpc             west           central      
     Min.   :0.00002   Min.   : 25.69   Min.   :0.0000   Min.   :0.0000  
     1st Qu.:0.54741   1st Qu.: 30.66   1st Qu.:0.0000   1st Qu.:0.0000  
     Median :0.96226   Median : 34.87   Median :0.0000   Median :0.0000  
     Mean   :1.42884   Mean   : 38.06   Mean   :0.2527   Mean   :0.3736  
     3rd Qu.:1.56824   3rd Qu.: 40.95   3rd Qu.:0.5000   3rd Qu.:1.0000  
     Max.   :8.82765   Max.   :119.76   Max.   :1.0000   Max.   :1.0000  
         urban            pctmin80           wcon            wtuc      
     Min.   :0.00000   Min.   : 1.284   Min.   :193.6   Min.   :187.6  
     1st Qu.:0.00000   1st Qu.: 9.845   1st Qu.:250.8   1st Qu.:374.6  
     Median :0.00000   Median :24.312   Median :281.4   Median :406.5  
     Mean   :0.08791   Mean   :25.495   Mean   :285.4   Mean   :411.7  
     3rd Qu.:0.00000   3rd Qu.:38.142   3rd Qu.:314.8   3rd Qu.:443.4  
     Max.   :1.00000   Max.   :64.348   Max.   :436.8   Max.   :613.2  
          wtrd            wfir            wser             wmfg      
     Min.   :154.2   Min.   :170.9   Min.   : 133.0   Min.   :157.4  
     1st Qu.:190.9   1st Qu.:286.5   1st Qu.: 229.7   1st Qu.:288.9  
     Median :203.0   Median :317.3   Median : 253.2   Median :320.2  
     Mean   :211.6   Mean   :322.1   Mean   : 275.6   Mean   :335.6  
     3rd Qu.:225.1   3rd Qu.:345.4   3rd Qu.: 280.5   3rd Qu.:359.6  
     Max.   :354.7   Max.   :509.5   Max.   :2177.1   Max.   :646.9  
          wfed            wsta            wloc            mix         
     Min.   :326.1   Min.   :258.3   Min.   :239.2   Min.   :0.01961  
     1st Qu.:400.2   1st Qu.:329.3   1st Qu.:297.3   1st Qu.:0.08073  
     Median :449.8   Median :357.7   Median :308.1   Median :0.10186  
     Mean   :442.9   Mean   :357.5   Mean   :312.7   Mean   :0.12884  
     3rd Qu.:478.0   3rd Qu.:382.6   3rd Qu.:329.2   3rd Qu.:0.15175  
     Max.   :598.0   Max.   :499.6   Max.   :388.1   Max.   :0.46512  
        pctymle       
     Min.   :0.06216  
     1st Qu.:0.07443  
     Median :0.07771  
     Mean   :0.08396  
     3rd Qu.:0.08350  
     Max.   :0.24871  


2. take out year column


```R
data_clean <- subset(data,select=-c(year))
objects(data_clean)
```


<ol class=list-inline>
	<li>'avgsen'</li>
	<li>'central'</li>
	<li>'county'</li>
	<li>'crmrte'</li>
	<li>'density'</li>
	<li>'mix'</li>
	<li>'pctmin80'</li>
	<li>'pctymle'</li>
	<li>'polpc'</li>
	<li>'prbarr'</li>
	<li>'prbconv'</li>
	<li>'prbpris'</li>
	<li>'taxpc'</li>
	<li>'urban'</li>
	<li>'wcon'</li>
	<li>'west'</li>
	<li>'wfed'</li>
	<li>'wfir'</li>
	<li>'wloc'</li>
	<li>'wmfg'</li>
	<li>'wser'</li>
	<li>'wsta'</li>
	<li>'wtrd'</li>
	<li>'wtuc'</li>
</ol>



3. "prbarr" max > 1


```R
hist(data$prbarr)
```


![png](output_15_0.png)



```R
data_clean <- subset(data_clean,data_clean$prbarr <1)
```


```R
hist(data_clean$prbarr)
```


![png](output_17_0.png)


4. "prbconv" strange characters and blank spaces; also the probability is bigger than 1 <br>
__this is taken care of in data import__



```R
data_clean <- subset(data_clean,data_clean$prbconv <1)
```

5. taxpc, what is the unit, what does it mean? Outlier at 119. Is the unit %?<br>
__Not sure what to do with this__


```R
hist(data_clean$taxpc, breaks=50)
```


![png](output_21_0.png)


no evidence to say whether the data has anomaly or not, and we are not sure what the data means

### EDA

1. distribution of crimes committed per person


```R
hist(data_clean$crmrte,breaks=50)
hist(log(data_clean$crmrte),breaks=50)
```


![png](output_25_0.png)



![png](output_25_1.png)



```R
hist(data_clean$mix,breaks=50)

```


![png](output_26_0.png)



```R
install.packages("corrplot")
```

    Installing package into 'D:/Users/Owner/Documents/R/win-library/3.5'
    (as 'lib' is unspecified)
    Warning message:
    "unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.5:
      cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.5/PACKAGES'"

    package 'corrplot' successfully unpacked and MD5 sums checked
    
    The downloaded binary packages are in
    	C:\Users\Owner\AppData\Local\Temp\RtmpiuEB7F\downloaded_packages
    


```R
# correlation plot
library(corrplot)
corrplot(cor(data_clean[,sapply(data_clean,is.numeric)]),is.corr=T,  type='upper',main = "Correlation Plot", tl.cex=1.5)
```


![png](output_28_0.png)



```R

```

Dependent variable: crmrte, mix

prbarr, prbconv

taxpc?

1. crmrte: prbarr, prbconv, wage variables are positively correlated
2. mix: prbarr, prbconv, wage variables are negatively correlated

Research Question: 

__Research Question__: <br>
How to reduce crime rate? <br>
1. sub-quest: how to reduce crime rate by increasing the arrest probability for non face-to-face crime

Logics:<br>
1. mix is positively correlated with prbarr
2. higher percentage of face-to-face crime positively correlates with higher prbarr
3. the percentage of non face-to-face crime is much higher


model 1: crmrte = $\beta_0 + \beta_1 * prbarr + \beta_2 * prbconv + \beta_3 * avgsen + \beta_4 * prbpris + u $ <br>

model 2: crmrte = $\beta_0 + \beta_1 * prbarr + \beta_2 * prbconv + \beta_3 * avgsen + \beta_4 * prbpris + u $ <br>
         prbarr = $\gamma_0 + \gamma_1 * mix + \gamma_2 * polpc v$ <br>

Based on the understanding of what each parameter stands for, we have chosen crmrte as the only dependent variable to use for our analysis. The variable is a direct indicator of average crime commited to North Carolina counties. To start with, we took a look at the distribution of the dataset


```R
options(repr.plot.height = 10, repr.plot.width = 12, repr.plot.pointsize = 32)

hist(data_clean$crmrte, breaks=20, main="Logorithm of Crime Per Capita")
```


![png](output_35_0.png)


The distribution of crmrte does not look particularly normal, we decided to take the logorithm of and replot the histogram


```R
hist(log(data$crmrte), breaks=20, main= "Logorithm of Crime Per Capita")
```


![png](output_37_0.png)


Looking at the other variables, and the simple correlation plot in initial EDA, we are proposing the explanatory variables that we believe contribute to crime rate: <br>
1. prbarr: the probability of arrest should be a direct contributing factor to crime rate. In other words, if people who have potential to commit a crime believe the chance of them getting arrested is small, then it might encourage them to commit a crime
2. prbconv: after getting arrested, getting suspects convicted are the only way to let them take the punishment they deserve. 
3. prbpris
4. avgsen: both probability of prison sentence reflect the severity of the punishment, which should directly impact the crime rate
<br>
With the above being proposed, we decided to take a look at the distribution of each explanatory variable


```R
hist(data_clean$prbarr,breaks=20,main="prbarr", xlab="prbarr")
```


![png](output_39_0.png)



```R
hist(data_clean$prbconv,breaks=20,main="prbconv", xlab="prbconv")
```


![png](output_40_0.png)



```R
hist(data_clean$prbpris,breaks=20,main="prbpris", xlab="prbpris")
```


![png](output_41_0.png)



```R
hist(data_clean$avgsen,breaks=20,main="avgsen", xlab="avgsen")
```


![png](output_42_0.png)


The above histograms of each explanatory variable all seem rather normally distributed, while the dependent variable seems rather skewed. However, after taking the log transformation, the dependent variable seems rather normally distributed. That being said, we need a log transformed version of the dependent varible to minimize the standard error. 


```R
data_clean$crmrte_log <- log(data_clean$crmrte)
```


```R
hist(data_clean$crmrte_log, breaks=20, main="log transformation of crime rate per capita")
```


![png](output_45_0.png)


### Fitting model 1: <br>
crmrte = $\beta_0 + \beta_1 * prbarr + \beta_2 * prbconv + \beta_3 * avgsen + \beta_4 * prbpris + u $ <br>


```R
install.packages("stargazer")
```

    Installing package into 'D:/Users/Owner/Documents/R/win-library/3.5'
    (as 'lib' is unspecified)
    Warning message:
    "unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.5:
      cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.5/PACKAGES'"

    package 'stargazer' successfully unpacked and MD5 sums checked
    
    The downloaded binary packages are in
    	C:\Users\Owner\AppData\Local\Temp\RtmpiuEB7F\downloaded_packages
    


```R
library(stargazer)
```

    
    Please cite as: 
    
     Hlavac, Marek (2018). stargazer: Well-Formatted Regression and Summary Statistics Tables.
     R package version 5.2.2. https://CRAN.R-project.org/package=stargazer 
    
    


```R
model1 <- lm(crmrte_log ~ prbarr + prbconv + avgsen + prbpris, data=data_clean)

```


```R
stargazer(model1)
```

    
    % Table created by stargazer v.5.2.2 by Marek Hlavac, Harvard University. E-mail: hlavac at fas.harvard.edu
    % Date and time: Fri, Nov 23, 2018 - 10:41:45 AM
    \begin{table}[!htbp] \centering 
      \caption{} 
      \label{} 
    \begin{tabular}{@{\extracolsep{5pt}}lc} 
    \\[-1.8ex]\hline 
    \hline \\[-1.8ex] 
     & \multicolumn{1}{c}{\textit{Dependent variable:}} \\ 
    \cline{2-2} 
    \\[-1.8ex] & crmrte\_log \\ 
    \hline \\[-1.8ex] 
     prbarr & $-$2.626$^{***}$ \\ 
      & (0.423) \\ 
      & \\ 
     prbconv & $-$0.962$^{***}$ \\ 
      & (0.268) \\ 
      & \\ 
     avgsen & 0.009 \\ 
      & (0.020) \\ 
      & \\ 
     prbpris & 0.100 \\ 
      & (0.589) \\ 
      & \\ 
     Constant & $-$2.385$^{***}$ \\ 
      & (0.402) \\ 
      & \\ 
    \hline \\[-1.8ex] 
    Observations & 81 \\ 
    R$^{2}$ & 0.390 \\ 
    Adjusted R$^{2}$ & 0.358 \\ 
    Residual Std. Error & 0.405 (df = 76) \\ 
    F Statistic & 12.156$^{***}$ (df = 4; 76) \\ 
    \hline 
    \hline \\[-1.8ex] 
    \textit{Note:}  & \multicolumn{1}{r}{$^{*}$p$<$0.1; $^{**}$p$<$0.05; $^{***}$p$<$0.01} \\ 
    \end{tabular} 
    \end{table} 
    


```R

```


```R

```


```R

```


```R

```


```R

```


```R

```


```R

```
