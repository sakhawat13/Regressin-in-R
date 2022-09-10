# Running Simple Regression with R

> ## Loading the data


```R
dataset = read.csv("Merged_w_ec_growth_data.xlsx")
```


```R
dataset
```


<table>
<thead><tr><th scope=col>X</th><th scope=col>zip</th><th scope=col>county</th><th scope=col>num_below_p50</th><th scope=col>pop2018</th><th scope=col>ec_zip</th><th scope=col>ec_se_zip</th><th scope=col>nbhd_ec_zip</th><th scope=col>ec_grp_mem_zip</th><th scope=col>ec_high_zip</th><th scope=col>...</th><th scope=col>bias_grp_mem_zip</th><th scope=col>bias_grp_mem_high_zip</th><th scope=col>nbhd_bias_zip</th><th scope=col>nbhd_bias_high_zip</th><th scope=col>clustering_zip</th><th scope=col>support_ratio_zip</th><th scope=col>volunteering_rate_zip</th><th scope=col>civic_organizations_zip</th><th scope=col>ESTAB</th><th scope=col>UID</th></tr></thead>
<tbody>
	<tr><td> 0          </td><td>1001        </td><td>25013       </td><td> 995.78747  </td><td>17621       </td><td>0.88157     </td><td>0.02422     </td><td>1.51095     </td><td>1.10210     </td><td>1.47136     </td><td>...         </td><td> 0.024340000</td><td>-0.10001    </td><td>-0.00336    </td><td>-0.21186    </td><td>0.10572000  </td><td>0.9452600   </td><td>0.05650000  </td><td>0.010800000 </td><td> 944        </td><td>2.018e+10   </td></tr>
	<tr><td> 1          </td><td>1002        </td><td>25015       </td><td>1312.11708  </td><td>30066       </td><td>1.18348     </td><td>0.02227     </td><td>0.97760     </td><td>1.23333     </td><td>1.62290     </td><td>...         </td><td> 0.098559998</td><td>-0.06421    </td><td> 0.18724    </td><td>-0.24353    </td><td>0.10340000  </td><td>0.9016300   </td><td>0.14951000  </td><td>0.036880001 </td><td>1076        </td><td>2.018e+10   </td></tr>
	<tr><td> 2          </td><td>1003        </td><td>25015       </td><td>        NA  </td><td>11238       </td><td>1.37536     </td><td>0.05046     </td><td>     NA     </td><td>1.44359     </td><td>1.65159     </td><td>...         </td><td> 0.024820000</td><td>-0.05143    </td><td>      NA    </td><td>      NA    </td><td>0.13650000  </td><td>0.7692400   </td><td>0.10501000  </td><td>0.080499999 </td><td>  37        </td><td>2.018e+10   </td></tr>
	<tr><td> 3          </td><td>1005        </td><td>25027       </td><td> 381.51974  </td><td> 4991       </td><td>1.15543     </td><td>0.03050     </td><td>1.46491     </td><td>1.30756     </td><td>1.47733     </td><td>...         </td><td> 0.008500001</td><td>-0.07246    </td><td>-0.00064    </td><td>-0.11397    </td><td>0.10554000  </td><td>0.9583700   </td><td>0.15862000  </td><td>0.021630000 </td><td> 178        </td><td>2.018e+10   </td></tr>
	<tr><td> 4          </td><td>1007        </td><td>25015       </td><td> 915.39667  </td><td>14967       </td><td>1.19240     </td><td>0.02046     </td><td>1.17985     </td><td>1.32294     </td><td>1.56812     </td><td>...         </td><td>-0.011880000</td><td>-0.11464    </td><td> 0.04162    </td><td>-0.21283    </td><td>0.10391000  </td><td>0.9487300   </td><td>0.13053000  </td><td>0.016899999 </td><td> 440        </td><td>2.018e+10   </td></tr>
	<tr><td> 5          </td><td>1008        </td><td>25013       </td><td>  90.72176  </td><td> 1197       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.12223626  </td><td>0.8760978   </td><td>0.05135186  </td><td>0.021193897 </td><td>  37        </td><td>2.018e+10   </td></tr>
	<tr><td> 6          </td><td>1010        </td><td>25013       </td><td> 312.54297  </td><td> 3739       </td><td>0.73856     </td><td>0.05810     </td><td>     NA     </td><td>     NA     </td><td>1.47973     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.09408000  </td><td>0.8930200   </td><td>0.08233000  </td><td>0.031709999 </td><td> 169        </td><td>2.018e+10   </td></tr>
	<tr><td> 7          </td><td>1011        </td><td>25013       </td><td> 104.81068  </td><td> 1448       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.11377750  </td><td>0.9404994   </td><td>0.06918624  </td><td>0.032719631 </td><td>  19        </td><td>2.018e+10   </td></tr>
	<tr><td> 8          </td><td>1013        </td><td>25013       </td><td>2616.55035  </td><td>23065       </td><td>0.69744     </td><td>0.01274     </td><td>0.53930     </td><td>0.75807     </td><td>1.23152     </td><td>...         </td><td> 0.136999990</td><td>-0.09613    </td><td> 0.20223    </td><td>-0.40365    </td><td>0.08648000  </td><td>0.8905700   </td><td>0.06191000  </td><td>0.009690000 </td><td> 649        </td><td>2.018e+10   </td></tr>
	<tr><td> 9          </td><td>1020        </td><td>25013       </td><td>2002.08249  </td><td>30097       </td><td>0.72701     </td><td>0.01397     </td><td>0.99817     </td><td>0.89329     </td><td>1.28291     </td><td>...         </td><td> 0.124500000</td><td>-0.13772    </td><td> 0.14469    </td><td>-0.28785    </td><td>0.09264000  </td><td>0.9327200   </td><td>0.06153000  </td><td>0.000780000 </td><td>1074        </td><td>2.018e+10   </td></tr>
	<tr><td>10          </td><td>1022        </td><td>25013       </td><td> 149.91133  </td><td> 2499       </td><td>0.79394     </td><td>0.04236     </td><td>     NA     </td><td>0.94845     </td><td>1.29843     </td><td>...         </td><td> 0.027120000</td><td>-0.11148    </td><td>      NA    </td><td>      NA    </td><td>0.08695000  </td><td>0.5018900   </td><td>0.05766000  </td><td>0.032830000 </td><td> 131        </td><td>2.018e+10   </td></tr>
	<tr><td>11          </td><td>1026        </td><td>25015       </td><td> 100.43624  </td><td>  954       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.10906969  </td><td>0.8613015   </td><td>0.12126616  </td><td>0.048653323 </td><td>  37        </td><td>2.018e+10   </td></tr>
	<tr><td>12          </td><td>1027        </td><td>25015       </td><td>1205.84813  </td><td>17848       </td><td>1.13870     </td><td>0.01947     </td><td>1.13732     </td><td>1.22668     </td><td>1.58017     </td><td>...         </td><td> 0.034490000</td><td>-0.09178    </td><td> 0.10926    </td><td>-0.15314    </td><td>0.09705000  </td><td>0.9448700   </td><td>0.16144000  </td><td>0.025359999 </td><td> 860        </td><td>2.018e+10   </td></tr>
	<tr><td>13          </td><td>1028        </td><td>25013       </td><td> 567.51112  </td><td>16200       </td><td>0.94025     </td><td>0.02639     </td><td>1.45878     </td><td>1.06200     </td><td>1.51818     </td><td>...         </td><td> 0.049520001</td><td>-0.09285    </td><td> 0.08563    </td><td>-0.14006    </td><td>0.10353000  </td><td>0.9567200   </td><td>0.06718000  </td><td>0.012160000 </td><td>1044        </td><td>2.018e+10   </td></tr>
	<tr><td>14          </td><td>1030        </td><td>25013       </td><td> 610.15929  </td><td>11123       </td><td>0.98905     </td><td>0.03012     </td><td>1.49931     </td><td>1.14082     </td><td>1.48308     </td><td>...         </td><td> 0.069839999</td><td>-0.09908    </td><td> 0.05411    </td><td>-0.12149    </td><td>0.10812000  </td><td>0.9359500   </td><td>0.06610000  </td><td>0.007500000 </td><td> 426        </td><td>2.018e+10   </td></tr>
	<tr><td>15          </td><td>1031        </td><td>25027       </td><td> 104.24417  </td><td> 1197       </td><td>1.15798     </td><td>0.04491     </td><td>     NA     </td><td>     NA     </td><td>1.41496     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.10759000  </td><td>0.9039300   </td><td>0.05749000  </td><td>0.019330001 </td><td>  37        </td><td>2.018e+10   </td></tr>
	<tr><td>16          </td><td>1033        </td><td>25015       </td><td> 402.13144  </td><td> 6333       </td><td>1.19631     </td><td>0.02792     </td><td>1.32119     </td><td>1.30264     </td><td>1.53943     </td><td>...         </td><td>-0.004310000</td><td>-0.11729    </td><td>-0.10154    </td><td>-0.24198    </td><td>0.10157000  </td><td>0.9390000   </td><td>0.09242000  </td><td>0.023170000 </td><td> 252        </td><td>2.018e+10   </td></tr>
	<tr><td>17          </td><td>1034        </td><td>25013       </td><td> 145.17563  </td><td> 2179       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.10141406  </td><td>0.9268361   </td><td>0.09207355  </td><td>0.033621322 </td><td>  60        </td><td>2.018e+10   </td></tr>
	<tr><td>18          </td><td>1035        </td><td>25015       </td><td> 218.29059  </td><td> 5310       </td><td>1.13185     </td><td>0.03480     </td><td>     NA     </td><td>1.30748     </td><td>1.61351     </td><td>...         </td><td> 0.012460000</td><td>-0.09120    </td><td>      NA    </td><td>      NA    </td><td>0.09729000  </td><td>0.9224600   </td><td>0.11243000  </td><td>0.137229990 </td><td> 621        </td><td>2.018e+10   </td></tr>
	<tr><td>19          </td><td>1036        </td><td>25013       </td><td> 269.57901  </td><td> 5191       </td><td>1.06871     </td><td>0.04787     </td><td>     NA     </td><td>1.23535     </td><td>1.52443     </td><td>...         </td><td>-0.013070000</td><td>-0.08307    </td><td>      NA    </td><td>      NA    </td><td>0.10727000  </td><td>0.9370500   </td><td>0.06713000  </td><td>0.021250000 </td><td> 237        </td><td>2.018e+10   </td></tr>
	<tr><td>20          </td><td>1038        </td><td>25015       </td><td> 103.98728  </td><td> 2867       </td><td>1.15936     </td><td>0.04840     </td><td>     NA     </td><td>1.31947     </td><td>1.59393     </td><td>...         </td><td>-0.035580002</td><td>-0.09930    </td><td>      NA    </td><td>      NA    </td><td>0.10542000  </td><td>0.9611200   </td><td>0.13269000  </td><td>0.039740000 </td><td> 127        </td><td>2.018e+10   </td></tr>
	<tr><td>21          </td><td>1039        </td><td>25015       </td><td> 111.99360  </td><td> 1042       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.09131002  </td><td>0.7076065   </td><td>0.20204093  </td><td>0.025376104 </td><td>  56        </td><td>2.018e+10   </td></tr>
	<tr><td>22          </td><td>1040        </td><td>25013       </td><td>7716.43727  </td><td>40376       </td><td>0.54841     </td><td>0.01105     </td><td>0.48269     </td><td>0.58591     </td><td>1.26553     </td><td>...         </td><td> 0.266150000</td><td>-0.13471    </td><td> 0.32872    </td><td>-0.60271    </td><td>0.08306000  </td><td>0.9673600   </td><td>0.07510000  </td><td>0.013700000 </td><td>1698        </td><td>2.018e+10   </td></tr>
	<tr><td>23          </td><td>1050        </td><td>25015       </td><td> 212.58434  </td><td> 2422       </td><td>1.21948     </td><td>0.03011     </td><td>     NA     </td><td>1.28382     </td><td>1.51228     </td><td>...         </td><td>-0.010690000</td><td>-0.09887    </td><td>      NA    </td><td>      NA    </td><td>0.11536000  </td><td>0.9543800   </td><td>0.09895000  </td><td>0.040050000 </td><td>  58        </td><td>2.018e+10   </td></tr>
	<tr><td>24          </td><td>1053        </td><td>25015       </td><td>  69.91505  </td><td> 1702       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.08974133  </td><td>0.5324615   </td><td>0.13541465  </td><td>0.005409759 </td><td>  58        </td><td>2.018e+10   </td></tr>
	<tr><td>25          </td><td>1054        </td><td>25011       </td><td> 139.82561  </td><td> 1983       </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>     NA     </td><td>...         </td><td>          NA</td><td>      NA    </td><td>      NA    </td><td>      NA    </td><td>0.09307798  </td><td>0.7355363   </td><td>0.20803298  </td><td>0.040462032 </td><td>  71        </td><td>2.018e+10   </td></tr>
	<tr><td>26          </td><td>1056        </td><td>25013       </td><td>1133.18018  </td><td>21336       </td><td>0.92282     </td><td>0.02158     </td><td>1.50828     </td><td>1.16878     </td><td>1.44359     </td><td>...         </td><td> 0.039400000</td><td>-0.09848    </td><td> 0.02606    </td><td>-0.13277    </td><td>0.11473000  </td><td>0.9745400   </td><td>0.06515000  </td><td>0.008550000 </td><td> 824        </td><td>2.018e+10   </td></tr>
	<tr><td>27          </td><td>1057        </td><td>25013       </td><td> 619.54785  </td><td> 8745       </td><td>1.02590     </td><td>0.04016     </td><td>     NA     </td><td>1.29907     </td><td>1.48875     </td><td>...         </td><td>-0.011920000</td><td>-0.08785    </td><td>      NA    </td><td>      NA    </td><td>0.11420000  </td><td>0.9626900   </td><td>0.09687000  </td><td>0.015550000 </td><td> 276        </td><td>2.018e+10   </td></tr>
	<tr><td>28          </td><td>1060        </td><td>25015       </td><td> 771.90119  </td><td>15779       </td><td>1.11224     </td><td>0.02204     </td><td>1.06218     </td><td>1.25475     </td><td>1.64944     </td><td>...         </td><td> 0.053259999</td><td>-0.07143    </td><td> 0.20273    </td><td>-0.17117    </td><td>0.09675000  </td><td>0.8860300   </td><td>0.21965000  </td><td>0.046030000 </td><td>1475        </td><td>2.018e+10   </td></tr>
	<tr><td>29          </td><td>1062        </td><td>25015       </td><td> 673.62626  </td><td>10495       </td><td>1.04111     </td><td>0.02651     </td><td>0.96244     </td><td>1.16021     </td><td>1.62642     </td><td>...         </td><td> 0.093610004</td><td>-0.09005    </td><td> 0.22486    </td><td>-0.23059    </td><td>0.09605000  </td><td>0.9075500   </td><td>0.16169000  </td><td>0.024420001 </td><td> 392        </td><td>2.018e+10   </td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>   </td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>22998      </td><td>99686      </td><td>2261       </td><td> 282.51971 </td><td> 3870      </td><td>1.04625    </td><td>0.02123    </td><td>0.74320    </td><td>0.94138    </td><td>1.33862    </td><td>...        </td><td> 0.06632   </td><td>-0.14854   </td><td> 0.13865   </td><td>-0.19774   </td><td>0.1217800  </td><td>0.9964200  </td><td>0.12306000 </td><td>0.027920000</td><td> 304       </td><td>20180035155</td></tr>
	<tr><td>22999      </td><td>99690      </td><td>2050       </td><td>  98.05400 </td><td>  189      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.2765136  </td><td>1.0000000  </td><td>0.12723790 </td><td>         NA</td><td>   7       </td><td>20180035159</td></tr>
	<tr><td>23000      </td><td>99701      </td><td>2090       </td><td>2654.18028 </td><td>17510      </td><td>1.02661    </td><td>0.01317    </td><td>0.97815    </td><td>1.04232    </td><td>1.31492    </td><td>...        </td><td> 0.11771   </td><td>-0.07878   </td><td> 0.17776   </td><td>-0.10311   </td><td>0.0994000  </td><td>0.9536600  </td><td>0.12662999 </td><td>0.032839999</td><td>2277       </td><td>20180035163</td></tr>
	<tr><td>23001      </td><td>99702      </td><td>2090       </td><td> 958.05182 </td><td> 3006      </td><td>1.19997    </td><td>0.02414    </td><td>     NA    </td><td>1.26211    </td><td>1.32296    </td><td>...        </td><td>-0.07695   </td><td>-0.14300   </td><td>      NA   </td><td>      NA   </td><td>0.0862000  </td><td>0.9098100  </td><td>0.08299000 </td><td>0.021369999</td><td>  44       </td><td>20180035164</td></tr>
	<tr><td>23002      </td><td>99703      </td><td>2090       </td><td>1142.71216 </td><td> 8859      </td><td>1.06534    </td><td>0.01756    </td><td>1.50004    </td><td>1.16419    </td><td>1.18894    </td><td>...        </td><td>-0.07340   </td><td>-0.14836   </td><td> 0.00293   </td><td>-0.05455   </td><td>0.0885100  </td><td>0.7689200  </td><td>0.05696000 </td><td>0.006350000</td><td>  68       </td><td>20180035165</td></tr>
	<tr><td>23003      </td><td>99705      </td><td>2090       </td><td>1686.66644 </td><td>22944      </td><td>1.14628    </td><td>0.01430    </td><td>1.34328    </td><td>1.21509    </td><td>1.34359    </td><td>...        </td><td> 0.03946   </td><td>-0.08241   </td><td> 0.07393   </td><td>-0.07396   </td><td>0.0883200  </td><td>0.9335200  </td><td>0.13407999 </td><td>0.011350000</td><td> 625       </td><td>20180035166</td></tr>
	<tr><td>23004      </td><td>99709      </td><td>2090       </td><td>1932.82329 </td><td>30428      </td><td>1.11244    </td><td>0.01532    </td><td>1.25777    </td><td>1.21285    </td><td>1.41337    </td><td>...        </td><td> 0.05016   </td><td>-0.09758   </td><td> 0.08147   </td><td>-0.10092   </td><td>0.0955800  </td><td>0.9490300  </td><td>0.14044000 </td><td>0.014450000</td><td>1375       </td><td>20180035170</td></tr>
	<tr><td>23005      </td><td>99712      </td><td>2090       </td><td> 676.48917 </td><td>14489      </td><td>1.16031    </td><td>0.01931    </td><td>1.37003    </td><td>1.27901    </td><td>1.40368    </td><td>...        </td><td>-0.01349   </td><td>-0.10838   </td><td> 0.03885   </td><td>-0.06987   </td><td>0.0899600  </td><td>0.8586500  </td><td>0.14997999 </td><td>0.007430000</td><td> 297       </td><td>20180035173</td></tr>
	<tr><td>23006      </td><td>99737      </td><td>2240       </td><td> 643.61877 </td><td> 4821      </td><td>1.05997    </td><td>0.02970    </td><td>1.39443    </td><td>1.31369    </td><td>1.27496    </td><td>...        </td><td>-0.07568   </td><td>-0.11125   </td><td>-0.07407   </td><td>-0.12341   </td><td>0.1059400  </td><td>0.9862100  </td><td>0.09221000 </td><td>0.032310002</td><td> 205       </td><td>20180035185</td></tr>
	<tr><td>23007      </td><td>99738      </td><td>2240       </td><td>  34.11414 </td><td>  103      </td><td>0.90773    </td><td>0.03433    </td><td>1.03549    </td><td>1.00790    </td><td>1.18721    </td><td>...        </td><td> 0.07201   </td><td>-0.08506   </td><td> 0.02964   </td><td>-0.15999   </td><td>0.1663000  </td><td>0.9966600  </td><td>0.14999001 </td><td>0.014380000</td><td>   6       </td><td>20180035186</td></tr>
	<tr><td>23008      </td><td>99746      </td><td>2290       </td><td>  88.97930 </td><td>  404      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.2514930  </td><td>0.9974543  </td><td>0.22854100 </td><td>         NA</td><td>  NA       </td><td>         NA</td></tr>
	<tr><td>23009      </td><td>99752      </td><td>2188       </td><td> 675.34010 </td><td> 3370      </td><td>0.88957    </td><td>0.02427    </td><td>0.93402    </td><td>0.93614    </td><td>1.11053    </td><td>...        </td><td> 0.05953   </td><td>-0.11355   </td><td> 0.07980   </td><td>-0.13557   </td><td>0.2089900  </td><td>0.9956300  </td><td>0.15080000 </td><td>0.012380000</td><td> 106       </td><td>20180035193</td></tr>
	<tr><td>23010      </td><td>99760      </td><td>2290       </td><td> 157.95328 </td><td>  605      </td><td>1.14435    </td><td>0.03651    </td><td>     NA    </td><td>1.27471    </td><td>1.43815    </td><td>...        </td><td>-0.06485   </td><td>-0.14770   </td><td>      NA   </td><td>      NA   </td><td>0.0911600  </td><td>0.9866000  </td><td>0.14552000 </td><td>0.021660000</td><td>  35       </td><td>20180035197</td></tr>
	<tr><td>23011      </td><td>99762      </td><td>2180       </td><td> 493.92923 </td><td> 4307      </td><td>0.90193    </td><td>0.02568    </td><td>1.02844    </td><td>1.01667    </td><td>1.31936    </td><td>...        </td><td> 0.13881   </td><td>-0.11368   </td><td> 0.17875   </td><td>-0.16326   </td><td>0.1726000  </td><td>0.9984100  </td><td>0.07446000 </td><td>0.029390000</td><td> 212       </td><td>20180035198</td></tr>
	<tr><td>23012      </td><td>99766      </td><td>2185       </td><td> 110.77861 </td><td>  625      </td><td>0.90713    </td><td>0.03335    </td><td>     NA    </td><td>0.86080    </td><td>1.07961    </td><td>...        </td><td> 0.03962   </td><td>-0.10277   </td><td>      NA   </td><td>      NA   </td><td>0.2504400  </td><td>0.9988500  </td><td>0.14655000 </td><td>         NA</td><td>   5       </td><td>20180035201</td></tr>
	<tr><td>23013      </td><td>99769      </td><td>2180       </td><td> 207.16373 </td><td>  921      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.4189288  </td><td>1.0000000  </td><td>0.03917960 </td><td>0.006955206</td><td>   3       </td><td>20180035203</td></tr>
	<tr><td>23014      </td><td>99772      </td><td>2180       </td><td> 174.99324 </td><td>  597      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.2870269  </td><td>0.9989010  </td><td>0.05080566 </td><td>         NA</td><td>   7       </td><td>20180035205</td></tr>
	<tr><td>23015      </td><td>99789      </td><td>2185       </td><td>  65.67589 </td><td>  469      </td><td>1.11113    </td><td>0.02535    </td><td>1.16879    </td><td>1.17902    </td><td>1.26655    </td><td>...        </td><td> 0.01203   </td><td>-0.09084   </td><td> 0.01613   </td><td>-0.11385   </td><td>0.2071000  </td><td>0.9992900  </td><td>0.25099000 </td><td>0.000420000</td><td>  11       </td><td>20180035213</td></tr>
	<tr><td>23016      </td><td>99801      </td><td>2110       </td><td>2069.27684 </td><td>30106      </td><td>1.10954    </td><td>0.01607    </td><td>1.26145    </td><td>1.21543    </td><td>1.45670    </td><td>...        </td><td> 0.07411   </td><td>-0.12270   </td><td> 0.07380   </td><td>-0.12887   </td><td>0.1111500  </td><td>0.9952300  </td><td>0.11730000 </td><td>0.027720001</td><td>2115       </td><td>20180035215</td></tr>
	<tr><td>23017      </td><td>99824      </td><td>2110       </td><td> 137.28667 </td><td> 2224      </td><td>1.17545    </td><td>0.03650    </td><td>     NA    </td><td>1.23878    </td><td>1.49796    </td><td>...        </td><td> 0.04670   </td><td>-0.10578   </td><td>      NA   </td><td>      NA   </td><td>0.1104400  </td><td>0.9055000  </td><td>0.14851999 </td><td>0.025260000</td><td>  56       </td><td>20180035220</td></tr>
	<tr><td>23018      </td><td>99825      </td><td>2105       </td><td>  18.29631 </td><td>   63      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.1585385  </td><td>0.9990779  </td><td>0.06785855 </td><td>0.006123060</td><td>  12       </td><td>20180035221</td></tr>
	<tr><td>23019      </td><td>99827      </td><td>2100       </td><td> 323.69077 </td><td> 2565      </td><td>1.16103    </td><td>0.02914    </td><td>0.80469    </td><td>1.03071    </td><td>1.42918    </td><td>...        </td><td>-0.02275   </td><td>-0.15745   </td><td> 0.01611   </td><td>-0.21642   </td><td>0.1224000  </td><td>0.9972900  </td><td>0.10087000 </td><td>0.065760002</td><td> 287       </td><td>20180035223</td></tr>
	<tr><td>23020      </td><td>99833      </td><td>2195       </td><td> 484.40515 </td><td> 3255      </td><td>1.04721    </td><td>0.02557    </td><td>0.92852    </td><td>1.00921    </td><td>1.35218    </td><td>...        </td><td>-0.00256   </td><td>-0.14167   </td><td>-0.03406   </td><td>-0.21637   </td><td>0.1526000  </td><td>0.9992700  </td><td>0.14737999 </td><td>0.039719999</td><td> 318       </td><td>20180035227</td></tr>
	<tr><td>23021      </td><td>99835      </td><td>2220       </td><td> 790.15790 </td><td> 8738      </td><td>1.14199    </td><td>0.01983    </td><td>1.07357    </td><td>1.14861    </td><td>1.42479    </td><td>...        </td><td> 0.00953   </td><td>-0.12930   </td><td> 0.04966   </td><td>-0.15935   </td><td>0.1163200  </td><td>0.9959300  </td><td>0.13909000 </td><td>0.035030000</td><td> 739       </td><td>20180035228</td></tr>
	<tr><td>23022      </td><td>99840      </td><td>2230       </td><td>  75.41914 </td><td> 1061      </td><td>1.11489    </td><td>0.04286    </td><td>     NA    </td><td>1.22142    </td><td>1.43376    </td><td>...        </td><td>-0.08429   </td><td>-0.15464   </td><td>      NA   </td><td>      NA   </td><td>0.1125500  </td><td>0.9993800  </td><td>0.09069000 </td><td>0.037319999</td><td> 242       </td><td>20180035229</td></tr>
	<tr><td>23023      </td><td>99901      </td><td>2130       </td><td>1192.29981 </td><td>13818      </td><td>0.99517    </td><td>0.01776    </td><td>0.88014    </td><td>0.95456    </td><td>1.29659    </td><td>...        </td><td> 0.05710   </td><td>-0.14293   </td><td> 0.07122   </td><td>-0.21950   </td><td>0.1347300  </td><td>0.9972000  </td><td>0.11883000 </td><td>0.029990001</td><td>1198       </td><td>20180035232</td></tr>
	<tr><td>23024      </td><td>99921      </td><td>2198       </td><td> 365.76866 </td><td> 1986      </td><td>0.87977    </td><td>0.03071    </td><td>0.74555    </td><td>0.82996    </td><td>1.18270    </td><td>...        </td><td> 0.06010   </td><td>-0.08759   </td><td> 0.08723   </td><td>-0.14339   </td><td>0.1556100  </td><td>0.9975200  </td><td>0.08404000 </td><td>0.032150000</td><td> 133       </td><td>20180035235</td></tr>
	<tr><td>23025      </td><td>99925      </td><td>2198       </td><td> 154.51384 </td><td>  927      </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>     NA    </td><td>...        </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>      NA   </td><td>0.1465793  </td><td>0.9922981  </td><td>0.12396049 </td><td>0.027728340</td><td>  46       </td><td>20180035238</td></tr>
	<tr><td>23026      </td><td>99926      </td><td>2198       </td><td> 311.01425 </td><td> 1635      </td><td>0.87888    </td><td>0.03618    </td><td>0.81081    </td><td>0.83409    </td><td>1.07167    </td><td>...        </td><td> 0.00877   </td><td>-0.07257   </td><td>-0.00480   </td><td>-0.09655   </td><td>0.2527400  </td><td>1.0000000  </td><td>0.14291000 </td><td>0.011250000</td><td>  21       </td><td>20180035239</td></tr>
	<tr><td>23027      </td><td>99929      </td><td>2275       </td><td> 313.28299 </td><td> 2484      </td><td>1.06344    </td><td>0.03122    </td><td>0.88864    </td><td>0.96641    </td><td>1.32997    </td><td>...        </td><td> 0.01350   </td><td>-0.14883   </td><td> 0.00069   </td><td>-0.24887   </td><td>0.1655800  </td><td>1.0000000  </td><td>0.10700000 </td><td>0.042479999</td><td> 192       </td><td>20180035241</td></tr>
</tbody>
</table>



> ## Simple regression with lm (dependant - Economic Connectedness, Independant - number of establishment )


```R
simple.fit = lm(ec_zip~ESTAB, data=dataset)
summary(simple.fit)
```


    
    Call:
    lm(formula = ec_zip ~ ESTAB, data = dataset)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -0.63080 -0.15217 -0.00553  0.14929  0.83816 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 8.644e-01  2.047e-03  422.26   <2e-16 ***
    ESTAB       2.329e-05  1.644e-06   14.17   <2e-16 ***
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    
    Residual standard error: 0.2174 on 18966 degrees of freedom
      (4060 observations deleted due to missingness)
    Multiple R-squared:  0.01048,	Adjusted R-squared:  0.01042 
    F-statistic: 200.8 on 1 and 18966 DF,  p-value: < 2.2e-16
    


### Results:
- Adjusted R is very low.
- p value is significant 
- coefficient value for ESTAB is still too low

> ## Simple regression with lm (dependant - High type Economic Connectedness with only neighbourhood freind, Independant - number of establishment )


```R
simpler.fit = lm(nbhd_ec_zip~ESTAB, data=dataset)
summary(simpler.fit)
```


    
    Call:
    lm(formula = nbhd_ec_zip ~ ESTAB, data = dataset)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -0.94852 -0.26253 -0.02595  0.23593  1.06854 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 7.830e-01  4.133e-03  189.46   <2e-16 ***
    ESTAB       6.146e-05  3.087e-06   19.91   <2e-16 ***
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    
    Residual standard error: 0.3562 on 14276 degrees of freedom
      (8750 observations deleted due to missingness)
    Multiple R-squared:  0.02702,	Adjusted R-squared:  0.02695 
    F-statistic: 396.5 on 1 and 14276 DF,  p-value: < 2.2e-16
    


### Results:
- Adjusted R is very low, but higher than the previous one. 
- p value is significant. 
- coefficient value for ESTAB is still too low, but higher than the previous one.
