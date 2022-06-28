---
id: litvis

narrative-schemas:
  - ../../lectures/narrative-schemas/project.yml

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest
---

@import "../../lectures/css/datavis.less"

```elm {l=hidden}
import Tidy exposing (..)
import VegaLite exposing (..)
```

```elm {l=hidden}
regionTable : Table
regionTable =
    """Entity,Year,Type of pollution,"Rate of death (per 100,000)"
African Region,1990,Indoor,201.9354892
African Region,1991,Indoor,199.2812226
African Region,1992,Indoor,197.5878132
African Region,1993,Indoor,195.1891706
African Region,1994,Indoor,192.9434158
African Region,1995,Indoor,190.884275
African Region,1996,Indoor,188.8692893
African Region,1997,Indoor,186.4180024
African Region,1998,Indoor,184.2376889
African Region,1999,Indoor,181.0489659
African Region,2000,Indoor,178.3511625
African Region,2001,Indoor,174.2523074
African Region,2002,Indoor,171.0934672
African Region,2003,Indoor,167.1667228
African Region,2004,Indoor,163.2037345
African Region,2005,Indoor,159.0107213
African Region,2006,Indoor,155.4917987
African Region,2007,Indoor,150.7703741
African Region,2008,Indoor,146.5047327
African Region,2009,Indoor,142.3554524
African Region,2010,Indoor,138.1356392
African Region,2011,Indoor,133.9126206
African Region,2012,Indoor,129.630144
African Region,2013,Indoor,125.0546827
African Region,2014,Indoor,120.5239249
African Region,2015,Indoor,117.0798081
African Region,2016,Indoor,113.6308641
African Region,2017,Indoor,110.3497462
African Region,2018,Indoor,107.0841608
African Region,2019,Indoor,103.3387132
African Region,1990,Outdoor,29.83895535
African Region,1991,Outdoor,30.09120381
African Region,1992,Outdoor,30.78493373
African Region,1993,Outdoor,30.95282249
African Region,1994,Outdoor,31.67878676
African Region,1995,Outdoor,32.18552859
African Region,1996,Outdoor,33.24174886
African Region,1997,Outdoor,34.93962684
African Region,1998,Outdoor,35.88345675
African Region,1999,Outdoor,36.46405729
African Region,2000,Outdoor,37.0882382
African Region,2001,Outdoor,36.98583661
African Region,2002,Outdoor,37.09120886
African Region,2003,Outdoor,37.02045107
African Region,2004,Outdoor,36.88603958
African Region,2005,Outdoor,36.81433381
African Region,2006,Outdoor,37.17716431
African Region,2007,Outdoor,37.41085375
African Region,2008,Outdoor,37.96094045
African Region,2009,Outdoor,38.65596679
African Region,2010,Outdoor,39.26845342
African Region,2011,Outdoor,40.21934323
African Region,2012,Outdoor,41.71003068
African Region,2013,Outdoor,43.25983533
African Region,2014,Outdoor,44.49250055
African Region,2015,Outdoor,45.20457487
African Region,2016,Outdoor,44.57695891
African Region,2017,Outdoor,43.84418493
African Region,2018,Outdoor,43.49840674
African Region,2019,Outdoor,43.87136477
African Region,1990,Air pollution (total),232.28506
African Region,1991,Air pollution (total),229.8411429
African Region,1992,Air pollution (total),228.7865882
African Region,1993,Air pollution (total),226.5381694
African Region,1994,Air pollution (total),225.0259907
African Region,1995,Air pollution (total),223.5721368
African Region,1996,Air pollution (total),222.6592228
African Region,1997,Air pollution (total),221.8787535
African Region,1998,Air pollution (total),220.5652278
African Region,1999,Air pollution (total),217.968232
African Region,2000,Air pollution (total),215.9078602
African Region,2001,Air pollution (total),211.7760305
African Region,2002,Air pollution (total),208.6409054
African Region,2003,Air pollution (total),204.5978342
African Region,2004,Air pollution (total),200.553878
African Region,2005,Air pollution (total),196.4631301
African Region,2006,Air pollution (total),193.5331722
African Region,2007,Air pollution (total),188.9456466
African Region,2008,Air pollution (total),185.0516393
African Region,2009,Air pollution (total),181.494403
African Region,2010,Air pollution (total),178.0250319
African Region,2011,Air pollution (total),174.895487
African Region,2012,Air pollution (total),172.0666715
African Region,2013,Air pollution (total),169.0254194
African Region,2014,Air pollution (total),165.6875465
African Region,2015,Air pollution (total),163.1505625
African Region,2016,Air pollution (total),159.082762
African Region,2017,Air pollution (total),155.063919
African Region,2018,Air pollution (total),151.6418913
African Region,2019,Air pollution (total),148.2782521
African Region,1990,Outdoor ozone pollution,1.681574531
African Region,1991,Outdoor ozone pollution,1.689858105
African Region,1992,Outdoor ozone pollution,1.613199138
African Region,1993,Outdoor ozone pollution,1.555906433
African Region,1994,Outdoor ozone pollution,1.453487541
African Region,1995,Outdoor ozone pollution,1.446290427
African Region,1996,Outdoor ozone pollution,1.399483754
African Region,1997,Outdoor ozone pollution,1.431398558
African Region,1998,Outdoor ozone pollution,1.399204407
African Region,1999,Outdoor ozone pollution,1.454096284
African Region,2000,Outdoor ozone pollution,1.173573672
African Region,2001,Outdoor ozone pollution,1.086046866
African Region,2002,Outdoor ozone pollution,0.907268116
African Region,2003,Outdoor ozone pollution,0.962571129
African Region,2004,Outdoor ozone pollution,1.190924226
African Region,2005,Outdoor ozone pollution,1.569117493
African Region,2006,Outdoor ozone pollution,2.066687771
African Region,2007,Outdoor ozone pollution,1.948635036
African Region,2008,Outdoor ozone pollution,1.61143461
African Region,2009,Outdoor ozone pollution,1.349832022
African Region,2010,Outdoor ozone pollution,1.431277664
African Region,2011,Outdoor ozone pollution,1.618827645
African Region,2012,Outdoor ozone pollution,1.735703734
African Region,2013,Outdoor ozone pollution,1.946346884
African Region,2014,Outdoor ozone pollution,1.914047493
African Region,2015,Outdoor ozone pollution,1.925257034
African Region,2016,Outdoor ozone pollution,1.802128365
African Region,2017,Outdoor ozone pollution,1.817639088
African Region,2018,Outdoor ozone pollution,2.127564093
African Region,2019,Outdoor ozone pollution,2.220023162
Eastern Mediterranean Region,1990,Indoor,127.8312391
Eastern Mediterranean Region,1991,Indoor,125.9605348
Eastern Mediterranean Region,1992,Indoor,124.3691371
Eastern Mediterranean Region,1993,Indoor,122.7560354
Eastern Mediterranean Region,1994,Indoor,121.0740902
Eastern Mediterranean Region,1995,Indoor,119.4377435
Eastern Mediterranean Region,1996,Indoor,116.30451
Eastern Mediterranean Region,1997,Indoor,112.6234663
Eastern Mediterranean Region,1998,Indoor,107.8433517
Eastern Mediterranean Region,1999,Indoor,103.5976249
Eastern Mediterranean Region,2000,Indoor,99.7434868
Eastern Mediterranean Region,2001,Indoor,96.20747722
Eastern Mediterranean Region,2002,Indoor,92.58803573
Eastern Mediterranean Region,2003,Indoor,89.24649656
Eastern Mediterranean Region,2004,Indoor,85.70832956
Eastern Mediterranean Region,2005,Indoor,82.04529992
Eastern Mediterranean Region,2006,Indoor,78.40761224
Eastern Mediterranean Region,2007,Indoor,74.47623026
Eastern Mediterranean Region,2008,Indoor,71.11954488
Eastern Mediterranean Region,2009,Indoor,67.57732214
Eastern Mediterranean Region,2010,Indoor,64.27671232
Eastern Mediterranean Region,2011,Indoor,60.95796488
Eastern Mediterranean Region,2012,Indoor,57.82446895
Eastern Mediterranean Region,2013,Indoor,55.03246042
Eastern Mediterranean Region,2014,Indoor,52.29407053
Eastern Mediterranean Region,2015,Indoor,49.85266095
Eastern Mediterranean Region,2016,Indoor,47.82266514
Eastern Mediterranean Region,2017,Indoor,45.7896599
Eastern Mediterranean Region,2018,Indoor,43.31592886
Eastern Mediterranean Region,2019,Indoor,40.67088308
Eastern Mediterranean Region,1990,Outdoor,74.31314034
Eastern Mediterranean Region,1991,Outdoor,75.44958709
Eastern Mediterranean Region,1992,Outdoor,76.57996106
Eastern Mediterranean Region,1993,Outdoor,78.47553426
Eastern Mediterranean Region,1994,Outdoor,80.02598936
Eastern Mediterranean Region,1995,Outdoor,80.81933929
Eastern Mediterranean Region,1996,Outdoor,81.89966148
Eastern Mediterranean Region,1997,Outdoor,84.23383376
Eastern Mediterranean Region,1998,Outdoor,86.42150298
Eastern Mediterranean Region,1999,Outdoor,88.17898486
Eastern Mediterranean Region,2000,Outdoor,88.10891916
Eastern Mediterranean Region,2001,Outdoor,89.60291486
Eastern Mediterranean Region,2002,Outdoor,90.88314156
Eastern Mediterranean Region,2003,Outdoor,92.30953239
Eastern Mediterranean Region,2004,Outdoor,92.18938488
Eastern Mediterranean Region,2005,Outdoor,91.8949138
Eastern Mediterranean Region,2006,Outdoor,92.43686834
Eastern Mediterranean Region,2007,Outdoor,93.11940904
Eastern Mediterranean Region,2008,Outdoor,94.73013414
Eastern Mediterranean Region,2009,Outdoor,96.02553751
Eastern Mediterranean Region,2010,Outdoor,96.53107862
Eastern Mediterranean Region,2011,Outdoor,96.31342154
Eastern Mediterranean Region,2012,Outdoor,97.17155163
Eastern Mediterranean Region,2013,Outdoor,97.79455302
Eastern Mediterranean Region,2014,Outdoor,98.27036461
Eastern Mediterranean Region,2015,Outdoor,99.34118513
Eastern Mediterranean Region,2016,Outdoor,98.04698218
Eastern Mediterranean Region,2017,Outdoor,96.2301527
Eastern Mediterranean Region,2018,Outdoor,95.85115544
Eastern Mediterranean Region,2019,Outdoor,96.34489953
Eastern Mediterranean Region,1990,Air pollution (total),204.338757
Eastern Mediterranean Region,1991,Air pollution (total),203.3508892
Eastern Mediterranean Region,1992,Air pollution (total),202.6961791
Eastern Mediterranean Region,1993,Air pollution (total),202.9557263
Eastern Mediterranean Region,1994,Air pollution (total),202.9847406
Eastern Mediterranean Region,1995,Air pollution (total),202.5862878
Eastern Mediterranean Region,1996,Air pollution (total),200.7662992
Eastern Mediterranean Region,1997,Air pollution (total),199.4653227
Eastern Mediterranean Region,1998,Air pollution (total),196.7976711
Eastern Mediterranean Region,1999,Air pollution (total),194.3984415
Eastern Mediterranean Region,2000,Air pollution (total),190.4935779
Eastern Mediterranean Region,2001,Air pollution (total),188.5097153
Eastern Mediterranean Region,2002,Air pollution (total),186.1151644
Eastern Mediterranean Region,2003,Air pollution (total),184.2803628
Eastern Mediterranean Region,2004,Air pollution (total),180.5618273
Eastern Mediterranean Region,2005,Air pollution (total),176.5928855
Eastern Mediterranean Region,2006,Air pollution (total),173.5282023
Eastern Mediterranean Region,2007,Air pollution (total),170.4348202
Eastern Mediterranean Region,2008,Air pollution (total),168.6902259
Eastern Mediterranean Region,2009,Air pollution (total),166.297436
Eastern Mediterranean Region,2010,Air pollution (total),163.4190767
Eastern Mediterranean Region,2011,Air pollution (total),159.9192275
Eastern Mediterranean Region,2012,Air pollution (total),157.5739506
Eastern Mediterranean Region,2013,Air pollution (total),155.41815
Eastern Mediterranean Region,2014,Air pollution (total),153.1166933
Eastern Mediterranean Region,2015,Air pollution (total),152.1375299
Eastern Mediterranean Region,2016,Air pollution (total),148.9977123
Eastern Mediterranean Region,2017,Air pollution (total),145.2253649
Eastern Mediterranean Region,2018,Air pollution (total),142.3883833
Eastern Mediterranean Region,2019,Air pollution (total),140.1925622
Eastern Mediterranean Region,1990,Outdoor ozone pollution,5.95106029
Eastern Mediterranean Region,1991,Outdoor ozone pollution,5.892804306
Eastern Mediterranean Region,1992,Outdoor ozone pollution,5.732228554
Eastern Mediterranean Region,1993,Outdoor ozone pollution,5.643058862
Eastern Mediterranean Region,1994,Outdoor ozone pollution,5.656731443
Eastern Mediterranean Region,1995,Outdoor ozone pollution,5.855182852
Eastern Mediterranean Region,1996,Outdoor ozone pollution,5.695415482
Eastern Mediterranean Region,1997,Outdoor ozone pollution,5.729910077
Eastern Mediterranean Region,1998,Outdoor ozone pollution,5.814289679
Eastern Mediterranean Region,1999,Outdoor ozone pollution,6.205678875
Eastern Mediterranean Region,2000,Outdoor ozone pollution,6.047819124
Eastern Mediterranean Region,2001,Outdoor ozone pollution,5.786313185
Eastern Mediterranean Region,2002,Outdoor ozone pollution,5.495227139
Eastern Mediterranean Region,2003,Outdoor ozone pollution,5.678627086
Eastern Mediterranean Region,2004,Outdoor ozone pollution,5.566505571
Eastern Mediterranean Region,2005,Outdoor ozone pollution,5.487324728
Eastern Mediterranean Region,2006,Outdoor ozone pollution,5.414471307
Eastern Mediterranean Region,2007,Outdoor ozone pollution,5.744202534
Eastern Mediterranean Region,2008,Outdoor ozone pollution,5.755484332
Eastern Mediterranean Region,2009,Outdoor ozone pollution,5.408896821
Eastern Mediterranean Region,2010,Outdoor ozone pollution,5.051914194
Eastern Mediterranean Region,2011,Outdoor ozone pollution,5.070064637
Eastern Mediterranean Region,2012,Outdoor ozone pollution,5.144105218
Eastern Mediterranean Region,2013,Outdoor ozone pollution,5.341985587
Eastern Mediterranean Region,2014,Outdoor ozone pollution,5.192645745
Eastern Mediterranean Region,2015,Outdoor ozone pollution,5.376695581
Eastern Mediterranean Region,2016,Outdoor ozone pollution,5.573469813
Eastern Mediterranean Region,2017,Outdoor ozone pollution,5.692020687
Eastern Mediterranean Region,2018,Outdoor ozone pollution,5.498817729
Eastern Mediterranean Region,2019,Outdoor ozone pollution,5.50619622
European Region,1990,Indoor,12.92347432
European Region,1991,Indoor,12.47708341
European Region,1992,Indoor,12.14157827
European Region,1993,Indoor,11.98947375
European Region,1994,Indoor,11.78288903
European Region,1995,Indoor,11.26179613
European Region,1996,Indoor,10.60256735
European Region,1997,Indoor,9.964532872
European Region,1998,Indoor,9.264864026
European Region,1999,Indoor,8.788195189
European Region,2000,Indoor,8.3270051
European Region,2001,Indoor,7.829199632
European Region,2002,Indoor,7.401706164
European Region,2003,Indoor,6.932187389
European Region,2004,Indoor,6.375614332
European Region,2005,Indoor,5.980683128
European Region,2006,Indoor,5.402881191
European Region,2007,Indoor,4.908033974
European Region,2008,Indoor,4.46656239
European Region,2009,Indoor,4.033817954
European Region,2010,Indoor,3.706485546
European Region,2011,Indoor,3.39598289
European Region,2012,Indoor,3.139332594
European Region,2013,Indoor,2.88457157
European Region,2014,Indoor,2.685509703
European Region,2015,Indoor,2.553736348
European Region,2016,Indoor,2.373034367
European Region,2017,Indoor,2.225656824
European Region,2018,Indoor,2.109364626
European Region,2019,Indoor,1.993373323
European Region,1990,Outdoor,58.17972607
European Region,1991,Outdoor,57.72334854
European Region,1992,Outdoor,57.85925776
European Region,1993,Outdoor,59.68617598
European Region,1994,Outdoor,60.24357084
European Region,1995,Outdoor,58.95564082
European Region,1996,Outdoor,56.54076689
European Region,1997,Outdoor,54.2549568
European Region,1998,Outdoor,52.13267546
European Region,1999,Outdoor,51.45083525
European Region,2000,Outdoor,50.07701558
European Region,2001,Outdoor,48.69494861
European Region,2002,Outdoor,47.92180094
European Region,2003,Outdoor,46.8325669
European Region,2004,Outdoor,44.74447252
European Region,2005,Outdoor,44.10403105
European Region,2006,Outdoor,42.01453651
European Region,2007,Outdoor,41.14620661
European Region,2008,Outdoor,40.81912668
European Region,2009,Outdoor,39.56594955
European Region,2010,Outdoor,38.73294285
European Region,2011,Outdoor,36.8771736
European Region,2012,Outdoor,35.27149447
European Region,2013,Outdoor,33.44404258
European Region,2014,Outdoor,31.75925154
European Region,2015,Outdoor,31.08036304
European Region,2016,Outdoor,29.04022482
European Region,2017,Outdoor,27.52748398
European Region,2018,Outdoor,27.29952539
European Region,2019,Outdoor,27.16719649
European Region,1990,Air pollution (total),72.88415679
European Region,1991,Air pollution (total),71.97396285
European Region,1992,Air pollution (total),71.69303196
European Region,1993,Air pollution (total),73.44753521
European Region,1994,Air pollution (total),73.79887262
European Region,1995,Air pollution (total),72.05422313
European Region,1996,Air pollution (total),68.85428402
European Region,1997,Air pollution (total),65.85325595
European Region,1998,Air pollution (total),62.95088899
European Region,1999,Air pollution (total),61.76284876
European Region,2000,Air pollution (total),59.84112255
European Region,2001,Air pollution (total),57.88278262
European Region,2002,Air pollution (total),56.82434573
European Region,2003,Air pollution (total),55.25868548
European Region,2004,Air pollution (total),52.57817894
European Region,2005,Air pollution (total),51.48482335
European Region,2006,Air pollution (total),48.82515843
European Region,2007,Air pollution (total),47.43410292
European Region,2008,Air pollution (total),46.57520534
European Region,2009,Air pollution (total),44.8228722
European Region,2010,Air pollution (total),43.61971431
European Region,2011,Air pollution (total),41.45661506
European Region,2012,Air pollution (total),39.60922758
European Region,2013,Air pollution (total),37.52007192
European Region,2014,Air pollution (total),35.61249148
European Region,2015,Air pollution (total),34.78584548
European Region,2016,Air pollution (total),32.52502831
European Region,2017,Air pollution (total),30.80085458
European Region,2018,Air pollution (total),30.51972872
European Region,2019,Air pollution (total),30.25388481
European Region,1990,Outdoor ozone pollution,2.176905321
European Region,1991,Outdoor ozone pollution,2.158293781
European Region,1992,Outdoor ozone pollution,2.058104104
European Region,1993,Outdoor ozone pollution,2.14980287
European Region,1994,Outdoor ozone pollution,2.143544298
European Region,1995,Outdoor ozone pollution,2.202811206
European Region,1996,Outdoor ozone pollution,2.035639662
European Region,1997,Outdoor ozone pollution,1.940862122
European Region,1998,Outdoor ozone pollution,1.844060347
European Region,1999,Outdoor ozone pollution,1.804726268
European Region,2000,Outdoor ozone pollution,1.690685207
European Region,2001,Outdoor ozone pollution,1.606962577
European Region,2002,Outdoor ozone pollution,1.803551025
European Region,2003,Outdoor ozone pollution,1.82166807
European Region,2004,Outdoor ozone pollution,1.765521626
European Region,2005,Outdoor ozone pollution,1.618548973
European Region,2006,Outdoor ozone pollution,1.560095804
European Region,2007,Outdoor ozone pollution,1.532664293
European Region,2008,Outdoor ozone pollution,1.465869132
European Region,2009,Outdoor ozone pollution,1.418318359
European Region,2010,Outdoor ozone pollution,1.366420457
European Region,2011,Outdoor ozone pollution,1.356104808
European Region,2012,Outdoor ozone pollution,1.377050516
European Region,2013,Outdoor ozone pollution,1.375270648
European Region,2014,Outdoor ozone pollution,1.344495137
European Region,2015,Outdoor ozone pollution,1.309102066
European Region,2016,Outdoor ozone pollution,1.25720012
European Region,2017,Outdoor ozone pollution,1.184839475
European Region,2018,Outdoor ozone pollution,1.240518515
European Region,2019,Outdoor ozone pollution,1.229462932
Region of the Americas,1990,Indoor,21.65952156
Region of the Americas,1991,Indoor,20.27201956
Region of the Americas,1992,Indoor,19.30663216
Region of the Americas,1993,Indoor,18.3650905
Region of the Americas,1994,Indoor,17.25078662
Region of the Americas,1995,Indoor,16.31320234
Region of the Americas,1996,Indoor,15.39096692
Region of the Americas,1997,Indoor,14.47983025
Region of the Americas,1998,Indoor,13.70676771
Region of the Americas,1999,Indoor,12.90111048
Region of the Americas,2000,Indoor,12.20892755
Region of the Americas,2001,Indoor,11.66697833
Region of the Americas,2002,Indoor,11.25160985
Region of the Americas,2003,Indoor,10.81206339
Region of the Americas,2004,Indoor,10.37207787
Region of the Americas,2005,Indoor,9.895911335
Region of the Americas,2006,Indoor,9.433918286
Region of the Americas,2007,Indoor,8.985114622
Region of the Americas,2008,Indoor,8.627775805
Region of the Americas,2009,Indoor,8.373898124
Region of the Americas,2010,Indoor,7.994722629
Region of the Americas,2011,Indoor,7.637627311
Region of the Americas,2012,Indoor,7.244548029
Region of the Americas,2013,Indoor,6.896476759
Region of the Americas,2014,Indoor,6.525975105
Region of the Americas,2015,Indoor,6.202468189
Region of the Americas,2016,Indoor,5.907757948
Region of the Americas,2017,Indoor,5.58175241
Region of the Americas,2018,Indoor,5.282810862
Region of the Americas,2019,Indoor,5.004349184
Region of the Americas,1990,Outdoor,33.07133027
Region of the Americas,1991,Outdoor,32.3102196
Region of the Americas,1992,Outdoor,31.8597093
Region of the Americas,1993,Outdoor,31.8853479
Region of the Americas,1994,Outdoor,31.44982058
Region of the Americas,1995,Outdoor,31.0925192
Region of the Americas,1996,Outdoor,30.52647056
Region of the Americas,1997,Outdoor,29.76572786
Region of the Americas,1998,Outdoor,29.28497988
Region of the Americas,1999,Outdoor,28.80311104
Region of the Americas,2000,Outdoor,27.94435911
Region of the Americas,2001,Outdoor,27.17474538
Region of the Americas,2002,Outdoor,26.55117053
Region of the Americas,2003,Outdoor,25.73315967
Region of the Americas,2004,Outdoor,24.61489545
Region of the Americas,2005,Outdoor,23.7806422
Region of the Americas,2006,Outdoor,22.98373341
Region of the Americas,2007,Outdoor,22.19831968
Region of the Americas,2008,Outdoor,21.67212991
Region of the Americas,2009,Outdoor,21.23463088
Region of the Americas,2010,Outdoor,20.57943228
Region of the Americas,2011,Outdoor,20.00994757
Region of the Americas,2012,Outdoor,19.49572871
Region of the Americas,2013,Outdoor,19.14143153
Region of the Americas,2014,Outdoor,18.70284795
Region of the Americas,2015,Outdoor,18.35797985
Region of the Americas,2016,Outdoor,17.91787884
Region of the Americas,2017,Outdoor,17.42481905
Region of the Americas,2018,Outdoor,17.32363161
Region of the Americas,2019,Outdoor,17.42604872
Region of the Americas,1990,Air pollution (total),56.56140192
Region of the Americas,1991,Air pollution (total),54.35436056
Region of the Americas,1992,Air pollution (total),52.93724488
Region of the Americas,1993,Air pollution (total),52.0444262
Region of the Americas,1994,Air pollution (total),50.63408586
Region of the Americas,1995,Air pollution (total),49.40648509
Region of the Americas,1996,Air pollution (total),47.92388427
Region of the Americas,1997,Air pollution (total),46.3198569
Region of the Americas,1998,Air pollution (total),45.20414021
Region of the Americas,1999,Air pollution (total),43.96604797
Region of the Americas,2000,Air pollution (total),42.29667625
Region of the Americas,2001,Air pollution (total),40.97273273
Region of the Americas,2002,Air pollution (total),39.93028677
Region of the Americas,2003,Air pollution (total),38.54938518
Region of the Americas,2004,Air pollution (total),36.87987064
Region of the Americas,2005,Air pollution (total),35.60585883
Region of the Americas,2006,Air pollution (total),34.44885205
Region of the Americas,2007,Air pollution (total),33.09954018
Region of the Americas,2008,Air pollution (total),32.03945867
Region of the Americas,2009,Air pollution (total),31.23973078
Region of the Americas,2010,Air pollution (total),30.22879456
Region of the Americas,2011,Air pollution (total),29.46445664
Region of the Americas,2012,Air pollution (total),28.52762812
Region of the Americas,2013,Air pollution (total),27.71464739
Region of the Americas,2014,Air pollution (total),26.75819112
Region of the Americas,2015,Air pollution (total),26.05704884
Region of the Americas,2016,Air pollution (total),25.33645027
Region of the Americas,2017,Air pollution (total),24.4250497
Region of the Americas,2018,Air pollution (total),24.11457433
Region of the Americas,2019,Air pollution (total),23.93558713
Region of the Americas,1990,Outdoor ozone pollution,2.142412812
Region of the Americas,1991,Outdoor ozone pollution,2.082461817
Region of the Americas,1992,Outdoor ozone pollution,2.093284115
Region of the Americas,1993,Outdoor ozone pollution,2.116290087
Region of the Americas,1994,Outdoor ozone pollution,2.26319018
Region of the Americas,1995,Outdoor ozone pollution,2.307490439
Region of the Americas,1996,Outdoor ozone pollution,2.28525856
Region of the Americas,1997,Outdoor ozone pollution,2.356733345
Region of the Americas,1998,Outdoor ozone pollution,2.521118903
Region of the Americas,1999,Outdoor ozone pollution,2.581902194
Region of the Americas,2000,Outdoor ozone pollution,2.418432992
Region of the Americas,2001,Outdoor ozone pollution,2.390927022
Region of the Americas,2002,Outdoor ozone pollution,2.388577644
Region of the Americas,2003,Outdoor ozone pollution,2.263729581
Region of the Americas,2004,Outdoor ozone pollution,2.129232071
Region of the Americas,2005,Outdoor ozone pollution,2.136568226
Region of the Americas,2006,Outdoor ozone pollution,2.228656613
Region of the Americas,2007,Outdoor ozone pollution,2.108035725
Region of the Americas,2008,Outdoor ozone pollution,1.930801345
Region of the Americas,2009,Outdoor ozone pollution,1.813207304
Region of the Americas,2010,Outdoor ozone pollution,1.809460781
Region of the Americas,2011,Outdoor ozone pollution,1.958478001
Region of the Americas,2012,Outdoor ozone pollution,1.948903231
Region of the Americas,2013,Outdoor ozone pollution,1.850640378
Region of the Americas,2014,Outdoor ozone pollution,1.698938795
Region of the Americas,2015,Outdoor ozone pollution,1.621719344
Region of the Americas,2016,Outdoor ozone pollution,1.624882793
Region of the Americas,2017,Outdoor ozone pollution,1.529883221
Region of the Americas,2018,Outdoor ozone pollution,1.62724971
Region of the Americas,2019,Outdoor ozone pollution,1.629126825
South-East Asia Region,1990,Indoor,198.4704623
South-East Asia Region,1991,Indoor,194.1382305
South-East Asia Region,1992,Indoor,189.8526127
South-East Asia Region,1993,Indoor,184.5627429
South-East Asia Region,1994,Indoor,178.7211498
South-East Asia Region,1995,Indoor,172.9210456
South-East Asia Region,1996,Indoor,169.7550761
South-East Asia Region,1997,Indoor,169.8206862
South-East Asia Region,1998,Indoor,165.4590651
South-East Asia Region,1999,Indoor,157.4750525
South-East Asia Region,2000,Indoor,152.7958287
South-East Asia Region,2001,Indoor,149.3945396
South-East Asia Region,2002,Indoor,145.28282
South-East Asia Region,2003,Indoor,138.4994003
South-East Asia Region,2004,Indoor,129.2360542
South-East Asia Region,2005,Indoor,126.3283402
South-East Asia Region,2006,Indoor,124.2241759
South-East Asia Region,2007,Indoor,120.2804496
South-East Asia Region,2008,Indoor,115.9039707
South-East Asia Region,2009,Indoor,107.1858586
South-East Asia Region,2010,Indoor,100.0037394
South-East Asia Region,2011,Indoor,93.89515884
South-East Asia Region,2012,Indoor,88.11374607
South-East Asia Region,2013,Indoor,83.73837602
South-East Asia Region,2014,Indoor,78.48137461
South-East Asia Region,2015,Indoor,73.4138609
South-East Asia Region,2016,Indoor,69.04694952
South-East Asia Region,2017,Indoor,65.92021047
South-East Asia Region,2018,Indoor,62.88325974
South-East Asia Region,2019,Indoor,58.53312205
South-East Asia Region,1990,Outdoor,51.50352873
South-East Asia Region,1991,Outdoor,51.89497055
South-East Asia Region,1992,Outdoor,52.19578816
South-East Asia Region,1993,Outdoor,52.33347481
South-East Asia Region,1994,Outdoor,52.38256799
South-East Asia Region,1995,Outdoor,52.35022987
South-East Asia Region,1996,Outdoor,53.53618481
South-East Asia Region,1997,Outdoor,56.1649865
South-East Asia Region,1998,Outdoor,57.91883865
South-East Asia Region,1999,Outdoor,58.48015698
South-East Asia Region,2000,Outdoor,59.85272425
South-East Asia Region,2001,Outdoor,61.21039622
South-East Asia Region,2002,Outdoor,62.2571766
South-East Asia Region,2003,Outdoor,62.21734398
South-East Asia Region,2004,Outdoor,61.09298958
South-East Asia Region,2005,Outdoor,62.9332394
South-East Asia Region,2006,Outdoor,65.56820558
South-East Asia Region,2007,Outdoor,67.84575374
South-East Asia Region,2008,Outdoor,70.15166821
South-East Asia Region,2009,Outdoor,69.47073578
South-East Asia Region,2010,Outdoor,69.59701807
South-East Asia Region,2011,Outdoor,71.66236783
South-East Asia Region,2012,Outdoor,74.75620747
South-East Asia Region,2013,Outdoor,79.62542985
South-East Asia Region,2014,Outdoor,82.14824078
South-East Asia Region,2015,Outdoor,81.6122442
South-East Asia Region,2016,Outdoor,79.48972466
South-East Asia Region,2017,Outdoor,78.45631968
South-East Asia Region,2018,Outdoor,80.2177342
South-East Asia Region,2019,Outdoor,81.78472027
South-East Asia Region,1990,Air pollution (total),252.9470688
South-East Asia Region,1991,Air pollution (total),248.9856927
South-East Asia Region,1992,Air pollution (total),244.9441711
South-East Asia Region,1993,Air pollution (total),239.9103568
South-East Asia Region,1994,Air pollution (total),234.2207632
South-East Asia Region,1995,Air pollution (total),228.7059844
South-East Asia Region,1996,Air pollution (total),226.9885703
South-East Asia Region,1997,Air pollution (total),230.0223064
South-East Asia Region,1998,Air pollution (total),227.5019303
South-East Asia Region,1999,Air pollution (total),220.1663333
South-East Asia Region,2000,Air pollution (total),216.7680794
South-East Asia Region,2001,Air pollution (total),214.8153519
South-East Asia Region,2002,Air pollution (total),211.595711
South-East Asia Region,2003,Air pollution (total),204.9684909
South-East Asia Region,2004,Air pollution (total),194.4558817
South-East Asia Region,2005,Air pollution (total),193.7541323
South-East Asia Region,2006,Air pollution (total),194.6371656
South-East Asia Region,2007,Air pollution (total),193.2891953
South-East Asia Region,2008,Air pollution (total),191.1735271
South-East Asia Region,2009,Air pollution (total),181.1925221
South-East Asia Region,2010,Air pollution (total),174.2007772
South-East Asia Region,2011,Air pollution (total),170.5677823
South-East Asia Region,2012,Air pollution (total),167.9561858
South-East Asia Region,2013,Air pollution (total),168.726093
South-East Asia Region,2014,Air pollution (total),166.0833485
South-East Asia Region,2015,Air pollution (total),161.0023139
South-East Asia Region,2016,Air pollution (total),154.6477868
South-East Asia Region,2017,Air pollution (total),150.6724758
South-East Asia Region,2018,Air pollution (total),149.9739991
South-East Asia Region,2019,Air pollution (total),147.1758692
South-East Asia Region,1990,Outdoor ozone pollution,10.32368865
South-East Asia Region,1991,Outdoor ozone pollution,10.44610806
South-East Asia Region,1992,Outdoor ozone pollution,10.3531584
South-East Asia Region,1993,Outdoor ozone pollution,10.59513257
South-East Asia Region,1994,Outdoor ozone pollution,10.5332568
South-East Asia Region,1995,Outdoor ozone pollution,10.74838592
South-East Asia Region,1996,Outdoor ozone pollution,10.87697615
South-East Asia Region,1997,Outdoor ozone pollution,11.68970129
South-East Asia Region,1998,Outdoor ozone pollution,12.03121265
South-East Asia Region,1999,Outdoor ozone pollution,12.39121737
South-East Asia Region,2000,Outdoor ozone pollution,11.97860093
South-East Asia Region,2001,Outdoor ozone pollution,11.95096586
South-East Asia Region,2002,Outdoor ozone pollution,11.46127085
South-East Asia Region,2003,Outdoor ozone pollution,11.83968258
South-East Asia Region,2004,Outdoor ozone pollution,11.29003364
South-East Asia Region,2005,Outdoor ozone pollution,11.71000974
South-East Asia Region,2006,Outdoor ozone pollution,12.26327445
South-East Asia Region,2007,Outdoor ozone pollution,13.10660938
South-East Asia Region,2008,Outdoor ozone pollution,13.108206
South-East Asia Region,2009,Outdoor ozone pollution,11.63405344
South-East Asia Region,2010,Outdoor ozone pollution,11.03247459
South-East Asia Region,2011,Outdoor ozone pollution,11.51675133
South-East Asia Region,2012,Outdoor ozone pollution,11.87125534
South-East Asia Region,2013,Outdoor ozone pollution,12.86992876
South-East Asia Region,2014,Outdoor ozone pollution,13.02905409
South-East Asia Region,2015,Outdoor ozone pollution,13.11993617
South-East Asia Region,2016,Outdoor ozone pollution,13.15840229
South-East Asia Region,2017,Outdoor ozone pollution,13.29022071
South-East Asia Region,2018,Outdoor ozone pollution,13.811225
South-East Asia Region,2019,Outdoor ozone pollution,13.94875244
Western Pacific Region,1990,Indoor,142.8399226
Western Pacific Region,1991,Indoor,136.9237345
Western Pacific Region,1992,Indoor,131.1474138
Western Pacific Region,1993,Indoor,125.1859813
Western Pacific Region,1994,Indoor,118.3796448
Western Pacific Region,1995,Indoor,111.4551992
Western Pacific Region,1996,Indoor,104.9868526
Western Pacific Region,1997,Indoor,97.69018575
Western Pacific Region,1998,Indoor,90.86334156
Western Pacific Region,1999,Indoor,85.79505667
Western Pacific Region,2000,Indoor,81.70799666
Western Pacific Region,2001,Indoor,77.16891974
Western Pacific Region,2002,Indoor,73.17763318
Western Pacific Region,2003,Indoor,69.16373412
Western Pacific Region,2004,Indoor,65.68444657
Western Pacific Region,2005,Indoor,61.07232709
Western Pacific Region,2006,Indoor,54.92715532
Western Pacific Region,2007,Indoor,49.71456258
Western Pacific Region,2008,Indoor,45.74867691
Western Pacific Region,2009,Indoor,42.32633503
Western Pacific Region,2010,Indoor,39.38507798
Western Pacific Region,2011,Indoor,36.34225163
Western Pacific Region,2012,Indoor,33.05412842
Western Pacific Region,2013,Indoor,30.26907038
Western Pacific Region,2014,Indoor,27.89660251
Western Pacific Region,2015,Indoor,25.74373846
Western Pacific Region,2016,Indoor,24.14649312
Western Pacific Region,2017,Indoor,22.59395479
Western Pacific Region,2018,Indoor,20.79011512
Western Pacific Region,2019,Indoor,18.81262162
Western Pacific Region,1990,Outdoor,60.42591473
Western Pacific Region,1991,Outdoor,60.92755738
Western Pacific Region,1992,Outdoor,61.57057286
Western Pacific Region,1993,Outdoor,62.32410484
Western Pacific Region,1994,Outdoor,62.68564459
Western Pacific Region,1995,Outdoor,63.10950336
Western Pacific Region,1996,Outdoor,63.76403874
Western Pacific Region,1997,Outdoor,64.33652978
Western Pacific Region,1998,Outdoor,65.20810492
Western Pacific Region,1999,Outdoor,66.7420736
Western Pacific Region,2000,Outdoor,68.30644846
Western Pacific Region,2001,Outdoor,68.7666547
Western Pacific Region,2002,Outdoor,69.35378239
Western Pacific Region,2003,Outdoor,69.62483647
Western Pacific Region,2004,Outdoor,70.41088324
Western Pacific Region,2005,Outdoor,69.92550084
Western Pacific Region,2006,Outdoor,67.667861
Western Pacific Region,2007,Outdoor,66.99446262
Western Pacific Region,2008,Outdoor,67.78689066
Western Pacific Region,2009,Outdoor,68.94390841
Western Pacific Region,2010,Outdoor,69.88507913
Western Pacific Region,2011,Outdoor,69.90125978
Western Pacific Region,2012,Outdoor,69.1025467
Western Pacific Region,2013,Outdoor,68.56509042
Western Pacific Region,2014,Outdoor,67.77152868
Western Pacific Region,2015,Outdoor,66.43855426
Western Pacific Region,2016,Outdoor,64.58405735
Western Pacific Region,2017,Outdoor,62.35399706
Western Pacific Region,2018,Outdoor,61.46255774
Western Pacific Region,2019,Outdoor,61.59113432
Western Pacific Region,1990,Air pollution (total),208.6386329
Western Pacific Region,1991,Air pollution (total),203.1732554
Western Pacific Region,1992,Air pollution (total),198.2863353
Western Pacific Region,1993,Air pollution (total),193.1600815
Western Pacific Region,1994,Air pollution (total),186.9685272
Western Pacific Region,1995,Air pollution (total),180.5429895
Western Pacific Region,1996,Air pollution (total),174.8326452
Western Pacific Region,1997,Air pollution (total),168.2129812
Western Pacific Region,1998,Air pollution (total),161.9479235
Western Pacific Region,1999,Air pollution (total),158.6255808
Western Pacific Region,2000,Air pollution (total),155.940076
Western Pacific Region,2001,Air pollution (total),151.8652518
Western Pacific Region,2002,Air pollution (total),148.2335501
Western Pacific Region,2003,Air pollution (total),144.517824
Western Pacific Region,2004,Air pollution (total),142.022323
Western Pacific Region,2005,Air pollution (total),136.8732498
Western Pacific Region,2006,Air pollution (total),128.597275
Western Pacific Region,2007,Air pollution (total),122.5888933
Western Pacific Region,2008,Air pollution (total),119.4815417
Western Pacific Region,2009,Air pollution (total),116.6682501
Western Pacific Region,2010,Air pollution (total),114.4295858
Western Pacific Region,2011,Air pollution (total),110.8324106
Western Pacific Region,2012,Air pollution (total),105.9549112
Western Pacific Region,2013,Air pollution (total),101.9011163
Western Pacific Region,2014,Air pollution (total),98.40095009
Western Pacific Region,2015,Air pollution (total),95.21256915
Western Pacific Region,2016,Air pollution (total),92.14450286
Western Pacific Region,2017,Air pollution (total),88.32531578
Western Pacific Region,2018,Air pollution (total),85.05639018
Western Pacific Region,2019,Air pollution (total),83.14125998
Western Pacific Region,1990,Outdoor ozone pollution,12.28780321
Western Pacific Region,1991,Outdoor ozone pollution,11.97852416
Western Pacific Region,1992,Outdoor ozone pollution,12.32294078
Western Pacific Region,1993,Outdoor ozone pollution,12.27806303
Western Pacific Region,1994,Outdoor ozone pollution,12.54331462
Western Pacific Region,1995,Outdoor ozone pollution,12.32812873
Western Pacific Region,1996,Outdoor ozone pollution,12.26210483
Western Pacific Region,1997,Outdoor ozone pollution,12.3224987
Western Pacific Region,1998,Outdoor ozone pollution,11.59622297
Western Pacific Region,1999,Outdoor ozone pollution,11.81224548
Western Pacific Region,2000,Outdoor ozone pollution,11.13882132
Western Pacific Region,2001,Outdoor ozone pollution,10.8684099
Western Pacific Region,2002,Outdoor ozone pollution,10.38818625
Western Pacific Region,2003,Outdoor ozone pollution,10.44672759
Western Pacific Region,2004,Outdoor ozone pollution,10.73542257
Western Pacific Region,2005,Outdoor ozone pollution,10.37439074
Western Pacific Region,2006,Outdoor ozone pollution,10.3577403
Western Pacific Region,2007,Outdoor ozone pollution,10.04302009
Western Pacific Region,2008,Outdoor ozone pollution,10.11636909
Western Pacific Region,2009,Outdoor ozone pollution,9.112751473
Western Pacific Region,2010,Outdoor ozone pollution,8.542316162
Western Pacific Region,2011,Outdoor ozone pollution,7.549484121
Western Pacific Region,2012,Outdoor ozone pollution,6.429868221
Western Pacific Region,2013,Outdoor ozone pollution,5.393027367
Western Pacific Region,2014,Outdoor ozone pollution,4.797714341
Western Pacific Region,2015,Outdoor ozone pollution,4.80828595
Western Pacific Region,2016,Outdoor ozone pollution,5.158482093
Western Pacific Region,2017,Outdoor ozone pollution,5.182491183
Western Pacific Region,2018,Outdoor ozone pollution,4.219354684
Western Pacific Region,2019,Outdoor ozone pollution,4.056302899
"""
        |> fromCSV
```

```elm {l=hidden}
geoTable : Table
geoTable =
    """Entity,Code,Year,Indoor deaths,Outdoor deaths,Latitude,Longitude,ID
Afghanistan,AFG,1990,370.0504743,37.40378629,33.93911,67.709953,4
Afghanistan,AFG,1991,358.9784184,36.09379659,33.93911,67.709953,4
Afghanistan,AFG,1992,352.7664528,35.12847416,33.93911,67.709953,4
Afghanistan,AFG,1993,357.0559225,35.2900467,33.93911,67.709953,4
Afghanistan,AFG,1994,362.9704392,35.87860142,33.93911,67.709953,4
Afghanistan,AFG,1995,363.2329649,36.05980786,33.93911,67.709953,4
Afghanistan,AFG,1996,364.6081627,36.06839043,33.93911,67.709953,4
Afghanistan,AFG,1997,367.3937773,36.26287438,33.93911,67.709953,4
Afghanistan,AFG,1998,369.8136956,36.54902213,33.93911,67.709953,4
Afghanistan,AFG,1999,372.2469924,37.09422641,33.93911,67.709953,4
Afghanistan,AFG,2000,371.9513445,37.22703334,33.93911,67.709953,4
Afghanistan,AFG,2001,368.4902535,36.76109905,33.93911,67.709953,4
Afghanistan,AFG,2002,355.8708514,35.68850097,33.93911,67.709953,4
Afghanistan,AFG,2003,350.1887476,35.98797976,33.93911,67.709953,4
Afghanistan,AFG,2004,341.8581056,35.95111029,33.93911,67.709953,4
Afghanistan,AFG,2005,331.0811191,35.76955129,33.93911,67.709953,4
Afghanistan,AFG,2006,320.2875784,36.07886629,33.93911,67.709953,4
Afghanistan,AFG,2007,306.5021038,38.23859535,33.93911,67.709953,4
Afghanistan,AFG,2008,292.5475289,40.49545506,33.93911,67.709953,4
Afghanistan,AFG,2009,278.2761753,42.11221384,33.93911,67.709953,4
Afghanistan,AFG,2010,265.0947492,43.54776237,33.93911,67.709953,4
Afghanistan,AFG,2011,252.4725103,46.36842166,33.93911,67.709953,4
Afghanistan,AFG,2012,239.7294396,50.76617397,33.93911,67.709953,4
Afghanistan,AFG,2013,227.3272139,55.04369706,33.93911,67.709953,4
Afghanistan,AFG,2014,216.5716077,57.92072757,33.93911,67.709953,4
Afghanistan,AFG,2015,208.0648033,59.41803469,33.93911,67.709953,4
Afghanistan,AFG,2016,200.6279496,59.10978672,33.93911,67.709953,4
Afghanistan,AFG,2017,194.3335609,59.11328315,33.93911,67.709953,4
Afghanistan,AFG,2018,187.2769889,59.54520299,33.93911,67.709953,4
Afghanistan,AFG,2019,179.4553489,61.94512723,33.93911,67.709953,4
Albania,ALB,1990,97.25254112,51.24363101,41.153332,20.168331,8
Albania,ALB,1991,98.11234817,50.41236961,41.153332,20.168331,8
Albania,ALB,1992,93.2941562,47.36086556,41.153332,20.168331,8
Albania,ALB,1993,88.00647596,44.54272888,41.153332,20.168331,8
Albania,ALB,1994,81.51332731,41.21547132,41.153332,20.168331,8
Albania,ALB,1995,81.76004257,41.18845661,41.153332,20.168331,8
Albania,ALB,1996,80.92313427,41.66509305,41.153332,20.168331,8
Albania,ALB,1997,76.9848265,42.26767971,41.153332,20.168331,8
Albania,ALB,1998,72.16222022,42.65746957,41.153332,20.168331,8
Albania,ALB,1999,68.40641519,43.44519692,41.153332,20.168331,8
Albania,ALB,2000,63.70081896,43.33951933,41.153332,20.168331,8
Albania,ALB,2001,57.58114465,41.69931134,41.153332,20.168331,8
Albania,ALB,2002,56.15543849,43.59296072,41.153332,20.168331,8
Albania,ALB,2003,55.71071423,46.45924864,41.153332,20.168331,8
Albania,ALB,2004,51.9697951,46.72287867,41.153332,20.168331,8
Albania,ALB,2005,47.43948942,45.72222024,41.153332,20.168331,8
Albania,ALB,2006,41.52145862,43.41621802,41.153332,20.168331,8
Albania,ALB,2007,36.12850971,41.79271246,41.153332,20.168331,8
Albania,ALB,2008,33.03456796,42.45403049,41.153332,20.168331,8
Albania,ALB,2009,29.49455349,41.84427458,41.153332,20.168331,8
Albania,ALB,2010,27.00723604,41.18960409,41.153332,20.168331,8
Albania,ALB,2011,25.55047755,41.12337093,41.153332,20.168331,8
Albania,ALB,2012,24.11283307,40.49466115,41.153332,20.168331,8
Albania,ALB,2013,22.96266251,39.97579333,41.153332,20.168331,8
Albania,ALB,2014,22.10134731,39.88566115,41.153332,20.168331,8
Albania,ALB,2015,21.2667667,39.70591103,41.153332,20.168331,8
Albania,ALB,2016,20.19794403,39.09789427,41.153332,20.168331,8
Albania,ALB,2017,19.23666919,38.52583111,41.153332,20.168331,8
Albania,ALB,2018,18.34878157,38.00771732,41.153332,20.168331,8
Albania,ALB,2019,17.54366701,37.50004557,41.153332,20.168331,8
Algeria,DZA,1990,28.32325041,106.2901565,28.033886,1.659626,12
Algeria,DZA,1991,24.38124994,105.2735045,28.033886,1.659626,12
Algeria,DZA,1992,21.23391561,105.7175252,28.033886,1.659626,12
Algeria,DZA,1993,18.46259998,106.5622844,28.033886,1.659626,12
Algeria,DZA,1994,16.06162681,107.6410692,28.033886,1.659626,12
Algeria,DZA,1995,13.91603623,108.4221741,28.033886,1.659626,12
Algeria,DZA,1996,11.98003853,108.9345485,28.033886,1.659626,12
Algeria,DZA,1997,10.21194327,109.7773602,28.033886,1.659626,12
Algeria,DZA,1998,8.60147177,109.6739724,28.033886,1.659626,12
Algeria,DZA,1999,7.336597695,111.0342904,28.033886,1.659626,12
Algeria,DZA,2000,6.217256114,109.4908972,28.033886,1.659626,12
Algeria,DZA,2001,5.274853363,106.9101135,28.033886,1.659626,12
Algeria,DZA,2002,4.449428544,104.0546736,28.033886,1.659626,12
Algeria,DZA,2003,3.732100357,101.1321419,28.033886,1.659626,12
Algeria,DZA,2004,3.129844202,98.67671157,28.033886,1.659626,12
Algeria,DZA,2005,2.625006974,95.97939882,28.033886,1.659626,12
Algeria,DZA,2006,2.192657323,93.52051259,28.033886,1.659626,12
Algeria,DZA,2007,1.810553371,90.92538069,28.033886,1.659626,12
Algeria,DZA,2008,1.483099001,88.46112686,28.033886,1.659626,12
Algeria,DZA,2009,1.214199734,86.47549592,28.033886,1.659626,12
Algeria,DZA,2010,1.007996494,84.81749222,28.033886,1.659626,12
Algeria,DZA,2011,0.852510386,84.24186583,28.033886,1.659626,12
Algeria,DZA,2012,0.716447699,83.58788305,28.033886,1.659626,12
Algeria,DZA,2013,0.601025556,83.21580623,28.033886,1.659626,12
Algeria,DZA,2014,0.509760422,83.31715154,28.033886,1.659626,12
Algeria,DZA,2015,0.434104843,83.08803178,28.033886,1.659626,12
Algeria,DZA,2016,0.370873238,80.89839211,28.033886,1.659626,12
Algeria,DZA,2017,0.320503344,79.34912416,28.033886,1.659626,12
Algeria,DZA,2018,0.275400145,79.21558916,28.033886,1.659626,12
Algeria,DZA,2019,0.233389392,79.11874593,28.033886,1.659626,12
American Samoa,ASM,1990,49.46355686,21.62902332,-14.270972,-170.132217,16
American Samoa,ASM,1991,45.4383581,22.34158843,-14.270972,-170.132217,16
American Samoa,ASM,1992,41.56577867,22.88474082,-14.270972,-170.132217,16
American Samoa,ASM,1993,38.01741637,23.19016463,-14.270972,-170.132217,16
American Samoa,ASM,1994,35.27862504,22.80846409,-14.270972,-170.132217,16
American Samoa,ASM,1995,33.2012199,22.29916082,-14.270972,-170.132217,16
American Samoa,ASM,1996,31.69829031,21.89761453,-14.270972,-170.132217,16
American Samoa,ASM,1997,30.54135942,21.53866122,-14.270972,-170.132217,16
American Samoa,ASM,1998,29.56416165,21.05034332,-14.270972,-170.132217,16
American Samoa,ASM,1999,28.74324541,20.37432493,-14.270972,-170.132217,16
American Samoa,ASM,2000,27.56834907,19.52518082,-14.270972,-170.132217,16
American Samoa,ASM,2001,26.18735546,19.33026559,-14.270972,-170.132217,16
American Samoa,ASM,2002,24.62006656,19.32157763,-14.270972,-170.132217,16
American Samoa,ASM,2003,23.07036229,19.21961753,-14.270972,-170.132217,16
American Samoa,ASM,2004,21.82531334,19.15174775,-14.270972,-170.132217,16
American Samoa,ASM,2005,21.20417885,18.94585885,-14.270972,-170.132217,16
American Samoa,ASM,2006,21.03061265,18.87641235,-14.270972,-170.132217,16
American Samoa,ASM,2007,20.88293448,18.40615814,-14.270972,-170.132217,16
American Samoa,ASM,2008,20.89825532,18.06764166,-14.270972,-170.132217,16
American Samoa,ASM,2009,20.90735654,17.65286884,-14.270972,-170.132217,16
American Samoa,ASM,2010,20.71991801,17.28309624,-14.270972,-170.132217,16
American Samoa,ASM,2011,20.29646021,17.16042155,-14.270972,-170.132217,16
American Samoa,ASM,2012,19.38268964,17.18088335,-14.270972,-170.132217,16
American Samoa,ASM,2013,18.23498606,17.54327885,-14.270972,-170.132217,16
American Samoa,ASM,2014,17.00459022,17.70057636,-14.270972,-170.132217,16
American Samoa,ASM,2015,16.0324835,17.94231362,-14.270972,-170.132217,16
American Samoa,ASM,2016,15.36245106,18.29841012,-14.270972,-170.132217,16
American Samoa,ASM,2017,14.70457637,18.42532124,-14.270972,-170.132217,16
American Samoa,ASM,2018,13.92913135,18.56324661,-14.270972,-170.132217,16
American Samoa,ASM,2019,13.06600529,18.19665606,-14.270972,-170.132217,16
Andorra,AND,1990,0.13544938,21.98417304,42.546245,1.601554,20
Andorra,AND,1991,0.122645411,21.06225499,42.546245,1.601554,20
Andorra,AND,1992,0.111494303,20.26976018,42.546245,1.601554,20
Andorra,AND,1993,0.099643216,19.50813159,42.546245,1.601554,20
Andorra,AND,1994,0.08992379,19.1085284,42.546245,1.601554,20
Andorra,AND,1995,0.080632001,18.86598683,42.546245,1.601554,20
Andorra,AND,1996,0.073101826,18.51002873,42.546245,1.601554,20
Andorra,AND,1997,0.066117011,18.11443341,42.546245,1.601554,20
Andorra,AND,1998,0.060211455,17.87823463,42.546245,1.601554,20
Andorra,AND,1999,0.054951394,17.84068837,42.546245,1.601554,20
Andorra,AND,2000,0.050305475,17.69933497,42.546245,1.601554,20
Andorra,AND,2001,0.045924576,17.17440994,42.546245,1.601554,20
Andorra,AND,2002,0.041811068,16.65701855,42.546245,1.601554,20
Andorra,AND,2003,0.038049253,15.83681681,42.546245,1.601554,20
Andorra,AND,2004,0.035163964,15.35349487,42.546245,1.601554,20
Andorra,AND,2005,0.032339724,14.77893415,42.546245,1.601554,20
Andorra,AND,2006,0.030034281,14.39124489,42.546245,1.601554,20
Andorra,AND,2007,0.027703824,13.73319758,42.546245,1.601554,20
Andorra,AND,2008,0.025819527,13.2743266,42.546245,1.601554,20
Andorra,AND,2009,0.024439111,13.07049245,42.546245,1.601554,20
Andorra,AND,2010,0.023210127,12.83830299,42.546245,1.601554,20
Andorra,AND,2011,0.022363946,12.59253812,42.546245,1.601554,20
Andorra,AND,2012,0.021615375,12.32247739,42.546245,1.601554,20
Andorra,AND,2013,0.021021262,12.11590437,42.546245,1.601554,20
Andorra,AND,2014,0.020327023,11.72434859,42.546245,1.601554,20
Andorra,AND,2015,0.019481583,11.18929333,42.546245,1.601554,20
Andorra,AND,2016,0.018363372,10.09406355,42.546245,1.601554,20
Andorra,AND,2017,0.01726033,9.218845697,42.546245,1.601554,20
Andorra,AND,2018,0.016474142,9.271895931,42.546245,1.601554,20
Andorra,AND,2019,0.015843427,9.148252607,42.546245,1.601554,20
Angola,AGO,1990,260.3436815,22.43476579,-11.202692,17.873887,24
Angola,AGO,1991,257.1207893,22.63647344,-11.202692,17.873887,24
Angola,AGO,1992,254.2702449,22.43813843,-11.202692,17.873887,24
Angola,AGO,1993,252.7825831,22.86184916,-11.202692,17.873887,24
Angola,AGO,1994,250.0300006,22.94015802,-11.202692,17.873887,24
Angola,AGO,1995,244.766957,23.17556264,-11.202692,17.873887,24
Angola,AGO,1996,236.7121789,23.19818007,-11.202692,17.873887,24
Angola,AGO,1997,230.2212414,23.99041341,-11.202692,17.873887,24
Angola,AGO,1998,226.1009959,25.14131293,-11.202692,17.873887,24
Angola,AGO,1999,221.0980594,26.28937214,-11.202692,17.873887,24
Angola,AGO,2000,214.5466088,26.13728948,-11.202692,17.873887,24
Angola,AGO,2001,205.8435522,26.18572437,-11.202692,17.873887,24
Angola,AGO,2002,197.4638336,25.88332312,-11.202692,17.873887,24
Angola,AGO,2003,191.7151954,26.5916294,-11.202692,17.873887,24
Angola,AGO,2004,188.1994178,28.25689811,-11.202692,17.873887,24
Angola,AGO,2005,178.7984395,29.23551432,-11.202692,17.873887,24
Angola,AGO,2006,171.5870164,30.66080071,-11.202692,17.873887,24
Angola,AGO,2007,162.1299099,30.54195979,-11.202692,17.873887,24
Angola,AGO,2008,154.9629398,30.87217359,-11.202692,17.873887,24
Angola,AGO,2009,146.9913144,31.48035877,-11.202692,17.873887,24
Angola,AGO,2010,139.0125536,32.52792528,-11.202692,17.873887,24
Angola,AGO,2011,130.5364147,33.97013498,-11.202692,17.873887,24
Angola,AGO,2012,121.6317933,35.72910667,-11.202692,17.873887,24
Angola,AGO,2013,111.7046377,37.54209183,-11.202692,17.873887,24
Angola,AGO,2014,100.9608219,38.72053036,-11.202692,17.873887,24
Angola,AGO,2015,93.21896628,40.26009604,-11.202692,17.873887,24
Angola,AGO,2016,85.65618387,41.47002641,-11.202692,17.873887,24
Angola,AGO,2017,79.09244459,42.95568963,-11.202692,17.873887,24
Angola,AGO,2018,73.49278625,44.85601602,-11.202692,17.873887,24
Angola,AGO,2019,68.3851746,47.10769147,-11.202692,17.873887,24
Antigua and Barbuda,ATG,1990,4.850842624,42.20230501,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1991,4.522628071,42.86467816,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1992,4.169588694,43.38569754,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1993,4.05802871,46.22122805,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1994,3.721680238,46.36648584,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1995,3.427015983,46.56954271,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1996,2.992974823,43.42224397,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1997,2.696333084,42.30021845,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1998,2.445661473,41.38160372,17.060816,-61.796428,28
Antigua and Barbuda,ATG,1999,2.232737841,40.56593679,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2000,2.036126171,39.34463245,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2001,1.887189909,38.18871201,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2002,1.749527029,36.50273805,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2003,1.635035081,35.04476963,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2004,1.535513053,33.78516299,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2005,1.438537339,32.93811084,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2006,1.358452722,32.84021088,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2007,1.381613457,36.0967309,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2008,1.299053524,35.92166478,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2009,1.155032238,33.46382482,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2010,1.08616093,33.40021891,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2011,1.020782879,33.53593398,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2012,0.949360877,33.55279223,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2013,0.889376178,33.89956617,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2014,0.841758795,34.72112834,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2015,0.78246823,34.79023353,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2016,0.719570896,33.64018521,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2017,0.658273098,32.49117802,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2018,0.60080805,32.35575167,17.060816,-61.796428,28
Antigua and Barbuda,ATG,2019,0.548651547,32.80599028,17.060816,-61.796428,28
Argentina,ARG,1990,12.8675216,37.53010237,-38.416097,-63.616672,32
Argentina,ARG,1991,11.74007318,37.07405696,-38.416097,-63.616672,32
Argentina,ARG,1992,10.87940619,37.14750967,-38.416097,-63.616672,32
Argentina,ARG,1993,9.890047612,36.37880933,-38.416097,-63.616672,32
Argentina,ARG,1994,8.878260718,35.11497401,-38.416097,-63.616672,32
Argentina,ARG,1995,8.229464038,34.79794074,-38.416097,-63.616672,32
Argentina,ARG,1996,7.616124296,34.19322326,-38.416097,-63.616672,32
Argentina,ARG,1997,7.067480137,33.34856292,-38.416097,-63.616672,32
Argentina,ARG,1998,6.640467446,32.89697572,-38.416097,-63.616672,32
Argentina,ARG,1999,6.195990114,32.13923156,-38.416097,-63.616672,32
Argentina,ARG,2000,5.547372443,30.19376015,-38.416097,-63.616672,32
Argentina,ARG,2001,5.137875595,29.42165116,-38.416097,-63.616672,32
Argentina,ARG,2002,4.817315285,29.11021687,-38.416097,-63.616672,32
Argentina,ARG,2003,4.486258221,28.58766471,-38.416097,-63.616672,32
Argentina,ARG,2004,4.025438239,27.16823211,-38.416097,-63.616672,32
Argentina,ARG,2005,3.618293555,26.17182072,-38.416097,-63.616672,32
Argentina,ARG,2006,3.307549365,25.78100441,-38.416097,-63.616672,32
Argentina,ARG,2007,3.095758541,26.25292666,-38.416097,-63.616672,32
Argentina,ARG,2008,2.746856027,25.28678887,-38.416097,-63.616672,32
Argentina,ARG,2009,2.514794855,25.21686953,-38.416097,-63.616672,32
Argentina,ARG,2010,2.344676744,25.4411015,-38.416097,-63.616672,32
Argentina,ARG,2011,2.182931743,25.65175178,-38.416097,-63.616672,32
Argentina,ARG,2012,2.024127697,25.82907205,-38.416097,-63.616672,32
Argentina,ARG,2013,1.894822224,25.9705189,-38.416097,-63.616672,32
Argentina,ARG,2014,1.763473721,25.89399941,-38.416097,-63.616672,32
Argentina,ARG,2015,1.669665872,26.09221189,-38.416097,-63.616672,32
Argentina,ARG,2016,1.610871637,26.16191244,-38.416097,-63.616672,32
Argentina,ARG,2017,1.507427505,24.97308641,-38.416097,-63.616672,32
Argentina,ARG,2018,1.389146368,24.43569529,-38.416097,-63.616672,32
Argentina,ARG,2019,1.307024658,24.18835346,-38.416097,-63.616672,32
Armenia,ARM,1990,38.4886483,91.5938945,40.069099,45.038189,51
Armenia,ARM,1991,39.99930077,95.14450942,40.069099,45.038189,51
Armenia,ARM,1992,43.8772353,104.0826501,40.069099,45.038189,51
Armenia,ARM,1993,45.58187463,108.6427646,40.069099,45.038189,51
Armenia,ARM,1994,43.02579458,103.5892903,40.069099,45.038189,51
Armenia,ARM,1995,41.95732947,101.6778943,40.069099,45.038189,51
Armenia,ARM,1996,41.2251998,101.0488098,40.069099,45.038189,51
Armenia,ARM,1997,38.26007291,95.87685603,40.069099,45.038189,51
Armenia,ARM,1998,36.27169149,93.81503605,40.069099,45.038189,51
Armenia,ARM,1999,34.58012146,93.99225934,40.069099,45.038189,51
Armenia,ARM,2000,32.02569011,91.83574947,40.069099,45.038189,51
Armenia,ARM,2001,29.77902486,92.29004956,40.069099,45.038189,51
Armenia,ARM,2002,26.61970843,93.54560743,40.069099,45.038189,51
Armenia,ARM,2003,23.34531373,95.83356764,40.069099,45.038189,51
Armenia,ARM,2004,19.52056269,95.73922636,40.069099,45.038189,51
Armenia,ARM,2005,16.46996002,96.36454389,40.069099,45.038189,51
Armenia,ARM,2006,13.86614784,97.52319682,40.069099,45.038189,51
Armenia,ARM,2007,11.05666236,96.57956487,40.069099,45.038189,51
Armenia,ARM,2008,8.884817516,98.08124824,40.069099,45.038189,51
Armenia,ARM,2009,7.003425898,97.67675229,40.069099,45.038189,51
Armenia,ARM,2010,5.693845414,96.18573128,40.069099,45.038189,51
Armenia,ARM,2011,4.813795624,94.92354979,40.069099,45.038189,51
Armenia,ARM,2012,4.073933102,92.73752364,40.069099,45.038189,51
Armenia,ARM,2013,3.453858104,89.9078704,40.069099,45.038189,51
Armenia,ARM,2014,3.045150934,89.35836774,40.069099,45.038189,51
Armenia,ARM,2015,2.768275135,89.72185384,40.069099,45.038189,51
Armenia,ARM,2016,2.500117566,86.37683341,40.069099,45.038189,51
Armenia,ARM,2017,2.318998887,83.89097666,40.069099,45.038189,51
Armenia,ARM,2018,2.144810889,82.60129628,40.069099,45.038189,51
Armenia,ARM,2019,1.978052438,81.40820227,40.069099,45.038189,51
Australia,AUS,1990,0.758338093,12.69971328,-25.274398,133.775136,36
Australia,AUS,1991,0.66908764,11.99561749,-25.274398,133.775136,36
Australia,AUS,1992,0.604802122,11.6170863,-25.274398,133.775136,36
Australia,AUS,1993,0.536103807,11.10997853,-25.274398,133.775136,36
Australia,AUS,1994,0.485865608,10.86151047,-25.274398,133.775136,36
Australia,AUS,1995,0.430335643,10.41313875,-25.274398,133.775136,36
Australia,AUS,1996,0.384541256,10.09983439,-25.274398,133.775136,36
Australia,AUS,1997,0.338130537,9.666877342,-25.274398,133.775136,36
Australia,AUS,1998,0.294465362,9.186518356,-25.274398,133.775136,36
Australia,AUS,1999,0.256315458,8.721891594,-25.274398,133.775136,36
Australia,AUS,2000,0.223470798,8.285286104,-25.274398,133.775136,36
Australia,AUS,2001,0.193234596,7.885038196,-25.274398,133.775136,36
Australia,AUS,2002,0.167530043,7.464417609,-25.274398,133.775136,36
Australia,AUS,2003,0.14239936,6.942860087,-25.274398,133.775136,36
Australia,AUS,2004,0.120548182,6.364442989,-25.274398,133.775136,36
Australia,AUS,2005,0.103492328,5.950070695,-25.274398,133.775136,36
Australia,AUS,2006,0.090866413,5.664114383,-25.274398,133.775136,36
Australia,AUS,2007,0.081517783,5.499510986,-25.274398,133.775136,36
Australia,AUS,2008,0.073160955,5.326489321,-25.274398,133.775136,36
Australia,AUS,2009,0.065006353,5.067292024,-25.274398,133.775136,36
Australia,AUS,2010,0.058328428,4.874297243,-25.274398,133.775136,36
Australia,AUS,2011,0.053363436,4.753933838,-25.274398,133.775136,36
Australia,AUS,2012,0.048465679,4.614494208,-25.274398,133.775136,36
Australia,AUS,2013,0.044728957,4.529805953,-25.274398,133.775136,36
Australia,AUS,2014,0.042037846,4.506738098,-25.274398,133.775136,36
Australia,AUS,2015,0.039263814,4.471412706,-25.274398,133.775136,36
Australia,AUS,2016,0.035498116,4.248385206,-25.274398,133.775136,36
Australia,AUS,2017,0.033043584,4.060651607,-25.274398,133.775136,36
Australia,AUS,2018,0.031765668,4.210068893,-25.274398,133.775136,36
Australia,AUS,2019,0.030455277,4.307855446,-25.274398,133.775136,36
Austria,AUT,1990,0.424021955,44.35454093,47.516231,14.550072,40
Austria,AUT,1991,0.39571401,43.90556055,47.516231,14.550072,40
Austria,AUT,1992,0.366401201,42.96750101,47.516231,14.550072,40
Austria,AUT,1993,0.338885247,41.94624015,47.516231,14.550072,40
Austria,AUT,1994,0.311091373,40.3462357,47.516231,14.550072,40
Austria,AUT,1995,0.289247219,39.25844704,47.516231,14.550072,40
Austria,AUT,1996,0.271867964,38.12676723,47.516231,14.550072,40
Austria,AUT,1997,0.250577667,36.13101846,47.516231,14.550072,40
Austria,AUT,1998,0.233476056,34.34976562,47.516231,14.550072,40
Austria,AUT,1999,0.216159329,32.59983929,47.516231,14.550072,40
Austria,AUT,2000,0.196023071,30.65325064,47.516231,14.550072,40
Austria,AUT,2001,0.177073384,29.1126396,47.516231,14.550072,40
Austria,AUT,2002,0.163761391,28.56428198,47.516231,14.550072,40
Austria,AUT,2003,0.151571823,27.86215083,47.516231,14.550072,40
Austria,AUT,2004,0.136100824,26.41266155,47.516231,14.550072,40
Austria,AUT,2005,0.124028138,25.13737648,47.516231,14.550072,40
Austria,AUT,2006,0.111637575,23.97918967,47.516231,14.550072,40
Austria,AUT,2007,0.101656385,23.14587399,47.516231,14.550072,40
Austria,AUT,2008,0.092228422,22.18946664,47.516231,14.550072,40
Austria,AUT,2009,0.085256004,21.61461386,47.516231,14.550072,40
Austria,AUT,2010,0.077743673,20.65527233,47.516231,14.550072,40
Austria,AUT,2011,0.072315935,19.76411737,47.516231,14.550072,40
Austria,AUT,2012,0.068084139,18.91905099,47.516231,14.550072,40
Austria,AUT,2013,0.064184202,17.91804822,47.516231,14.550072,40
Austria,AUT,2014,0.060462485,16.89528947,47.516231,14.550072,40
Austria,AUT,2015,0.057488689,16.04500542,47.516231,14.550072,40
Austria,AUT,2016,0.053269651,14.58904861,47.516231,14.550072,40
Austria,AUT,2017,0.049262734,13.45745058,47.516231,14.550072,40
Austria,AUT,2018,0.046641023,13.4299567,47.516231,14.550072,40
Austria,AUT,2019,0.044587536,13.59295441,47.516231,14.550072,40
Azerbaijan,AZE,1990,75.86461937,71.59643633,40.143105,47.576927,31
Azerbaijan,AZE,1991,77.43062133,76.72578861,40.143105,47.576927,31
Azerbaijan,AZE,1992,80.56841899,83.8091455,40.143105,47.576927,31
Azerbaijan,AZE,1993,83.09777998,90.42797918,40.143105,47.576927,31
Azerbaijan,AZE,1994,84.83347171,96.21475896,40.143105,47.576927,31
Azerbaijan,AZE,1995,82.30267691,96.90964802,40.143105,47.576927,31
Azerbaijan,AZE,1996,78.43683638,95.40411046,40.143105,47.576927,31
Azerbaijan,AZE,1997,73.93092019,93.37350681,40.143105,47.576927,31
Azerbaijan,AZE,1998,70.05580099,92.45670706,40.143105,47.576927,31
Azerbaijan,AZE,1999,66.12000721,92.06170503,40.143105,47.576927,31
Azerbaijan,AZE,2000,61.95577953,91.59095846,40.143105,47.576927,31
Azerbaijan,AZE,2001,56.75402615,90.05959361,40.143105,47.576927,31
Azerbaijan,AZE,2002,52.97898264,91.91238693,40.143105,47.576927,31
Azerbaijan,AZE,2003,49.49944844,95.04656836,40.143105,47.576927,31
Azerbaijan,AZE,2004,44.94283827,96.77586291,40.143105,47.576927,31
Azerbaijan,AZE,2005,41.41383942,100.6640148,40.143105,47.576927,31
Azerbaijan,AZE,2006,36.81456011,103.8375261,40.143105,47.576927,31
Azerbaijan,AZE,2007,31.41703447,106.7706734,40.143105,47.576927,31
Azerbaijan,AZE,2008,26.39419465,110.4961932,40.143105,47.576927,31
Azerbaijan,AZE,2009,22.21299416,113.4372161,40.143105,47.576927,31
Azerbaijan,AZE,2010,19.38689323,115.5457772,40.143105,47.576927,31
Azerbaijan,AZE,2011,17.5702147,117.3632033,40.143105,47.576927,31
Azerbaijan,AZE,2012,16.10053865,119.2503749,40.143105,47.576927,31
Azerbaijan,AZE,2013,14.88528969,120.4232881,40.143105,47.576927,31
Azerbaijan,AZE,2014,14.00364564,122.364971,40.143105,47.576927,31
Azerbaijan,AZE,2015,12.98250953,121.9488004,40.143105,47.576927,31
Azerbaijan,AZE,2016,12.16103108,120.3898568,40.143105,47.576927,31
Azerbaijan,AZE,2017,11.43833421,118.4481796,40.143105,47.576927,31
Azerbaijan,AZE,2018,10.23231885,112.5568201,40.143105,47.576927,31
Azerbaijan,AZE,2019,9.38676446,110.7646777,40.143105,47.576927,31
The Bahamas,BHS,1990,5.222176447,40.15345418,25.03428,-77.39628,44
The Bahamas,BHS,1991,4.915275918,39.38640062,25.03428,-77.39628,44
The Bahamas,BHS,1992,4.631348248,38.839423,25.03428,-77.39628,44
The Bahamas,BHS,1993,4.403316454,38.84693731,25.03428,-77.39628,44
The Bahamas,BHS,1994,4.152656967,38.7344178,25.03428,-77.39628,44
The Bahamas,BHS,1995,3.851539511,38.29329259,25.03428,-77.39628,44
The Bahamas,BHS,1996,3.657572851,39.33029124,25.03428,-77.39628,44
The Bahamas,BHS,1997,3.185877128,38.15117144,25.03428,-77.39628,44
The Bahamas,BHS,1998,2.806990429,37.97799108,25.03428,-77.39628,44
The Bahamas,BHS,1999,2.559247813,38.92095901,25.03428,-77.39628,44
The Bahamas,BHS,2000,2.22373077,36.89260048,25.03428,-77.39628,44
The Bahamas,BHS,2001,2.074896358,36.65819191,25.03428,-77.39628,44
The Bahamas,BHS,2002,1.869796076,34.64323498,25.03428,-77.39628,44
The Bahamas,BHS,2003,1.751792058,33.85405141,25.03428,-77.39628,44
The Bahamas,BHS,2004,1.641377799,33.1959197,25.03428,-77.39628,44
The Bahamas,BHS,2005,1.452531163,30.98703809,25.03428,-77.39628,44
The Bahamas,BHS,2006,1.338671672,30.47434394,25.03428,-77.39628,44
The Bahamas,BHS,2007,1.178485176,28.67104684,25.03428,-77.39628,44
The Bahamas,BHS,2008,1.093263039,28.47865584,25.03428,-77.39628,44
The Bahamas,BHS,2009,1.038372117,28.92442172,25.03428,-77.39628,44
The Bahamas,BHS,2010,0.955310363,28.46783042,25.03428,-77.39628,44
The Bahamas,BHS,2011,0.899799955,28.41645129,25.03428,-77.39628,44
The Bahamas,BHS,2012,0.842341074,28.27958211,25.03428,-77.39628,44
The Bahamas,BHS,2013,0.796378398,28.19296961,25.03428,-77.39628,44
The Bahamas,BHS,2014,0.752698814,28.21088324,25.03428,-77.39628,44
The Bahamas,BHS,2015,0.724078661,28.71323973,25.03428,-77.39628,44
The Bahamas,BHS,2016,0.686466904,27.93688209,25.03428,-77.39628,44
The Bahamas,BHS,2017,0.647539275,27.09221168,25.03428,-77.39628,44
The Bahamas,BHS,2018,0.615294404,27.25852478,25.03428,-77.39628,44
The Bahamas,BHS,2019,0.584013012,27.53961007,25.03428,-77.39628,44
Bahrain,BHR,1990,17.79624304,203.4611849,25.930414,50.637772,48
Bahrain,BHR,1991,16.12467186,203.873836,25.930414,50.637772,48
Bahrain,BHR,1992,14.26990521,200.0377342,25.930414,50.637772,48
Bahrain,BHR,1993,12.23752052,191.1191175,25.930414,50.637772,48
Bahrain,BHR,1994,10.5960694,187.1050864,25.930414,50.637772,48
Bahrain,BHR,1995,9.360793016,187.3385209,25.930414,50.637772,48
Bahrain,BHR,1996,8.368776521,189.6259863,25.930414,50.637772,48
Bahrain,BHR,1997,7.240356976,188.5889956,25.930414,50.637772,48
Bahrain,BHR,1998,6.300456372,189.7840399,25.930414,50.637772,48
Bahrain,BHR,1999,5.479361917,189.7470721,25.930414,50.637772,48
Bahrain,BHR,2000,4.169380567,166.4128014,25.930414,50.637772,48
Bahrain,BHR,2001,3.111492313,143.7463961,25.930414,50.637772,48
Bahrain,BHR,2002,2.997133592,164.1005691,25.930414,50.637772,48
Bahrain,BHR,2003,2.800561836,183.545411,25.930414,50.637772,48
Bahrain,BHR,2004,2.394375673,184.2457982,25.930414,50.637772,48
Bahrain,BHR,2005,2.049426898,181.5658284,25.930414,50.637772,48
Bahrain,BHR,2006,1.742266234,174.0505675,25.930414,50.637772,48
Bahrain,BHR,2007,1.480083475,166.8479075,25.930414,50.637772,48
Bahrain,BHR,2008,1.266589336,159.3811669,25.930414,50.637772,48
Bahrain,BHR,2009,1.082473635,150.2046362,25.930414,50.637772,48
Bahrain,BHR,2010,0.939402798,143.4415508,25.930414,50.637772,48
Bahrain,BHR,2011,0.823611428,138.8140333,25.930414,50.637772,48
Bahrain,BHR,2012,0.726146263,135.9827876,25.930414,50.637772,48
Bahrain,BHR,2013,0.616224601,126.7572059,25.930414,50.637772,48
Bahrain,BHR,2014,0.521820161,117.6407731,25.930414,50.637772,48
Bahrain,BHR,2015,0.458084896,113.8334694,25.930414,50.637772,48
Bahrain,BHR,2016,0.421743974,113.0429036,25.930414,50.637772,48
Bahrain,BHR,2017,0.389640523,112.8563106,25.930414,50.637772,48
Bahrain,BHR,2018,0.338620075,109.8584714,25.930414,50.637772,48
Bahrain,BHR,2019,0.288910768,108.7559116,25.930414,50.637772,48
Bangladesh,BGD,1990,249.2863531,41.95902609,23.684994,90.356331,50
Bangladesh,BGD,1991,228.0474606,40.36316973,23.684994,90.356331,50
Bangladesh,BGD,1992,223.2266143,41.43240965,23.684994,90.356331,50
Bangladesh,BGD,1993,216.2595088,42.93318662,23.684994,90.356331,50
Bangladesh,BGD,1994,209.6263095,43.70745433,23.684994,90.356331,50
Bangladesh,BGD,1995,207.4792128,45.79693664,23.684994,90.356331,50
Bangladesh,BGD,1996,199.8215755,46.67977443,23.684994,90.356331,50
Bangladesh,BGD,1997,191.9842169,47.98087289,23.684994,90.356331,50
Bangladesh,BGD,1998,188.4524119,49.78590734,23.684994,90.356331,50
Bangladesh,BGD,1999,186.932235,51.87229429,23.684994,90.356331,50
Bangladesh,BGD,2000,187.4407337,53.46376009,23.684994,90.356331,50
Bangladesh,BGD,2001,184.9947175,53.65854378,23.684994,90.356331,50
Bangladesh,BGD,2002,187.4003856,55.05997432,23.684994,90.356331,50
Bangladesh,BGD,2003,188.7097043,57.2485406,23.684994,90.356331,50
Bangladesh,BGD,2004,185.894679,57.61640957,23.684994,90.356331,50
Bangladesh,BGD,2005,184.7686673,58.82048809,23.684994,90.356331,50
Bangladesh,BGD,2006,183.3389219,60.69828747,23.684994,90.356331,50
Bangladesh,BGD,2007,175.6585909,61.98844372,23.684994,90.356331,50
Bangladesh,BGD,2008,164.4144123,61.52637478,23.684994,90.356331,50
Bangladesh,BGD,2009,155.5293414,61.1448468,23.684994,90.356331,50
Bangladesh,BGD,2010,148.7224012,62.81114108,23.684994,90.356331,50
Bangladesh,BGD,2011,129.5768156,60.01915883,23.684994,90.356331,50
Bangladesh,BGD,2012,112.9534819,58.91083159,23.684994,90.356331,50
Bangladesh,BGD,2013,104.6160924,61.4551303,23.684994,90.356331,50
Bangladesh,BGD,2014,100.3938196,65.31724009,23.684994,90.356331,50
Bangladesh,BGD,2015,93.38283069,64.64676194,23.684994,90.356331,50
Bangladesh,BGD,2016,89.5049878,64.30295752,23.684994,90.356331,50
Bangladesh,BGD,2017,89.29571092,66.9332856,23.684994,90.356331,50
Bangladesh,BGD,2018,84.67409591,68.34009904,23.684994,90.356331,50
Bangladesh,BGD,2019,79.25479103,70.62985389,23.684994,90.356331,50
Barbados,BRB,1990,0.288639576,50.59766682,13.193887,-59.543198,52
Barbados,BRB,1991,0.261319742,49.51103557,13.193887,-59.543198,52
Barbados,BRB,1992,0.244660725,50.16224687,13.193887,-59.543198,52
Barbados,BRB,1993,0.226404449,50.08409856,13.193887,-59.543198,52
Barbados,BRB,1994,0.210276123,49.98501999,13.193887,-59.543198,52
Barbados,BRB,1995,0.196289752,49.41290807,13.193887,-59.543198,52
Barbados,BRB,1996,0.183326734,48.46437368,13.193887,-59.543198,52
Barbados,BRB,1997,0.173937684,47.98550426,13.193887,-59.543198,52
Barbados,BRB,1998,0.162981056,46.46914762,13.193887,-59.543198,52
Barbados,BRB,1999,0.151034189,44.28623654,13.193887,-59.543198,52
Barbados,BRB,2000,0.143923631,43.76147238,13.193887,-59.543198,52
Barbados,BRB,2001,0.130523589,41.25868704,13.193887,-59.543198,52
Barbados,BRB,2002,0.125837742,41.23906736,13.193887,-59.543198,52
Barbados,BRB,2003,0.121150846,41.19840169,13.193887,-59.543198,52
Barbados,BRB,2004,0.11291182,39.83839326,13.193887,-59.543198,52
Barbados,BRB,2005,0.103041606,37.9717364,13.193887,-59.543198,52
Barbados,BRB,2006,0.09639356,37.42517795,13.193887,-59.543198,52
Barbados,BRB,2007,0.090822505,37.07785713,13.193887,-59.543198,52
Barbados,BRB,2008,0.084264188,36.16831616,13.193887,-59.543198,52
Barbados,BRB,2009,0.077173931,34.68555156,13.193887,-59.543198,52
Barbados,BRB,2010,0.071923779,34.21288995,13.193887,-59.543198,52
Barbados,BRB,2011,0.067722205,34.41884521,13.193887,-59.543198,52
Barbados,BRB,2012,0.062365698,34.3842928,13.193887,-59.543198,52
Barbados,BRB,2013,0.058784311,35.23124708,13.193887,-59.543198,52
Barbados,BRB,2014,0.05569748,36.09042401,13.193887,-59.543198,52
Barbados,BRB,2015,0.052653024,36.36654,13.193887,-59.543198,52
Barbados,BRB,2016,0.049957288,35.52286788,13.193887,-59.543198,52
Barbados,BRB,2017,0.047494286,34.72534848,13.193887,-59.543198,52
Barbados,BRB,2018,0.045251723,35.13653173,13.193887,-59.543198,52
Barbados,BRB,2019,0.043501555,36.56955317,13.193887,-59.543198,52
Belarus,BLR,1990,7.45852602,87.06173051,53.709807,27.953389,112
Belarus,BLR,1991,7.162246066,88.68195511,53.709807,27.953389,112
Belarus,BLR,1992,6.883964392,90.04037015,53.709807,27.953389,112
Belarus,BLR,1993,7.011951236,97.07602764,53.709807,27.953389,112
Belarus,BLR,1994,6.656719245,96.8559063,53.709807,27.953389,112
Belarus,BLR,1995,6.47647016,99.32244118,53.709807,27.953389,112
Belarus,BLR,1996,6.064650648,97.06395117,53.709807,27.953389,112
Belarus,BLR,1997,5.867095808,97.06335224,53.709807,27.953389,112
Belarus,BLR,1998,5.665240683,97.23121587,53.709807,27.953389,112
Belarus,BLR,1999,5.520242378,98.46136267,53.709807,27.953389,112
Belarus,BLR,2000,4.942845257,92.50561386,53.709807,27.953389,112
Belarus,BLR,2001,4.82023583,95.63094117,53.709807,27.953389,112
Belarus,BLR,2002,4.713650545,99.42402475,53.709807,27.953389,112
Belarus,BLR,2003,4.22333944,95.47566598,53.709807,27.953389,112
Belarus,BLR,2004,3.795957261,92.65098489,53.709807,27.953389,112
Belarus,BLR,2005,3.5028075,93.69625202,53.709807,27.953389,112
Belarus,BLR,2006,3.010664942,90.16255354,53.709807,27.953389,112
Belarus,BLR,2007,2.482602265,85.68692652,53.709807,27.953389,112
Belarus,BLR,2008,2.103386923,85.68917162,53.709807,27.953389,112
Belarus,BLR,2009,1.806677618,86.54173777,53.709807,27.953389,112
Belarus,BLR,2010,1.579479928,86.87688708,53.709807,27.953389,112
Belarus,BLR,2011,1.431016258,86.82420731,53.709807,27.953389,112
Belarus,BLR,2012,1.151816425,75.28003074,53.709807,27.953389,112
Belarus,BLR,2013,1.023909064,71.01637282,53.709807,27.953389,112
Belarus,BLR,2014,0.913885284,66.66217419,53.709807,27.953389,112
Belarus,BLR,2015,0.814019447,61.8978108,53.709807,27.953389,112
Belarus,BLR,2016,0.750788701,57.2150322,53.709807,27.953389,112
Belarus,BLR,2017,0.700074492,54.29472395,53.709807,27.953389,112
Belarus,BLR,2018,0.63934172,53.10660942,53.709807,27.953389,112
Belarus,BLR,2019,0.594864423,52.85253619,53.709807,27.953389,112
Belgium,BEL,1990,0.291096458,46.446941,50.503887,4.469936,112
Belgium,BEL,1991,0.260759671,44.58264005,50.503887,4.469936,112
Belgium,BEL,1992,0.236430181,42.82236339,50.503887,4.469936,112
Belgium,BEL,1993,0.216089417,42.20498674,50.503887,4.469936,112
Belgium,BEL,1994,0.19489842,40.6007295,50.503887,4.469936,112
Belgium,BEL,1995,0.178158953,39.65005901,50.503887,4.469936,112
Belgium,BEL,1996,0.163768335,38.12702435,50.503887,4.469936,112
Belgium,BEL,1997,0.150833774,36.52136156,50.503887,4.469936,112
Belgium,BEL,1998,0.140224199,35.3286053,50.503887,4.469936,112
Belgium,BEL,1999,0.129420797,33.7663753,50.503887,4.469936,112
Belgium,BEL,2000,0.117911173,32.16322568,50.503887,4.469936,112
Belgium,BEL,2001,0.106651434,30.2638739,50.503887,4.469936,112
Belgium,BEL,2002,0.098291016,29.81329794,50.503887,4.469936,112
Belgium,BEL,2003,0.089453909,28.52663239,50.503887,4.469936,112
Belgium,BEL,2004,0.078972033,26.73997795,50.503887,4.469936,112
Belgium,BEL,2005,0.07095935,25.45397822,50.503887,4.469936,112
Belgium,BEL,2006,0.062954588,24.30379222,50.503887,4.469936,112
Belgium,BEL,2007,0.057131537,24.1260287,50.503887,4.469936,112
Belgium,BEL,2008,0.051978036,24.0073937,50.503887,4.469936,112
Belgium,BEL,2009,0.047075634,23.86254731,50.503887,4.469936,112
Belgium,BEL,2010,0.042469275,23.2166544,50.503887,4.469936,112
Belgium,BEL,2011,0.038865633,22.06019402,50.503887,4.469936,112
Belgium,BEL,2012,0.036100718,20.77963868,50.503887,4.469936,112
Belgium,BEL,2013,0.033219225,19.04173201,50.503887,4.469936,112
Belgium,BEL,2014,0.03005555,17.13906534,50.503887,4.469936,112
Belgium,BEL,2015,0.02829054,16.14406286,50.503887,4.469936,112
Belgium,BEL,2016,0.026160519,15.28122348,50.503887,4.469936,112
Belgium,BEL,2017,0.024937522,14.9835373,50.503887,4.469936,112
Belgium,BEL,2018,0.023699403,15.00439509,50.503887,4.469936,112
Belgium,BEL,2019,0.022547927,14.96494896,50.503887,4.469936,112
Belize,BLZ,1990,51.45748498,27.43980132,17.189877,-88.49765,84
Belize,BLZ,1991,45.17707801,27.59259266,17.189877,-88.49765,84
Belize,BLZ,1992,41.26450874,28.70407484,17.189877,-88.49765,84
Belize,BLZ,1993,38.72005209,30.17421993,17.189877,-88.49765,84
Belize,BLZ,1994,36.91164978,31.92135309,17.189877,-88.49765,84
Belize,BLZ,1995,36.03229992,34.10242246,17.189877,-88.49765,84
Belize,BLZ,1996,36.42575706,37.00361055,17.189877,-88.49765,84
Belize,BLZ,1997,37.31887589,40.54852803,17.189877,-88.49765,84
Belize,BLZ,1998,37.49490384,43.68019549,17.189877,-88.49765,84
Belize,BLZ,1999,37.50003106,46.58368203,17.189877,-88.49765,84
Belize,BLZ,2000,36.69799295,47.55105349,17.189877,-88.49765,84
Belize,BLZ,2001,32.25065243,43.29290969,17.189877,-88.49765,84
Belize,BLZ,2002,29.25837338,40.36604228,17.189877,-88.49765,84
Belize,BLZ,2003,27.62587945,39.40827624,17.189877,-88.49765,84
Belize,BLZ,2004,26.45855015,38.69113323,17.189877,-88.49765,84
Belize,BLZ,2005,24.82381886,37.34359565,17.189877,-88.49765,84
Belize,BLZ,2006,23.82983235,36.80267474,17.189877,-88.49765,84
Belize,BLZ,2007,22.14611376,35.0390201,17.189877,-88.49765,84
Belize,BLZ,2008,20.14752836,32.68162214,17.189877,-88.49765,84
Belize,BLZ,2009,19.27681622,32.14748636,17.189877,-88.49765,84
Belize,BLZ,2010,18.520307,32.08742359,17.189877,-88.49765,84
Belize,BLZ,2011,17.4134983,32.07428315,17.189877,-88.49765,84
Belize,BLZ,2012,16.10591759,32.65101104,17.189877,-88.49765,84
Belize,BLZ,2013,15.34614724,34.0867271,17.189877,-88.49765,84
Belize,BLZ,2014,14.76612372,35.7064257,17.189877,-88.49765,84
Belize,BLZ,2015,14.03961977,36.22592083,17.189877,-88.49765,84
Belize,BLZ,2016,13.10364556,35.19027437,17.189877,-88.49765,84
Belize,BLZ,2017,12.34748176,34.51109645,17.189877,-88.49765,84
Belize,BLZ,2018,11.8956901,35.54701925,17.189877,-88.49765,84
Belize,BLZ,2019,11.18486587,36.21735567,17.189877,-88.49765,84
Benin,BEN,1990,247.4222182,23.45160825,9.30769,2.315834,204
Benin,BEN,1991,243.833548,23.35767719,9.30769,2.315834,204
Benin,BEN,1992,239.824088,23.22469862,9.30769,2.315834,204
Benin,BEN,1993,235.6556047,23.21759023,9.30769,2.315834,204
Benin,BEN,1994,233.354859,23.32090936,9.30769,2.315834,204
Benin,BEN,1995,230.7238503,23.63069153,9.30769,2.315834,204
Benin,BEN,1996,228.2839887,24.5148027,9.30769,2.315834,204
Benin,BEN,1997,223.2620078,25.76558905,9.30769,2.315834,204
Benin,BEN,1998,218.8970392,27.14749901,9.30769,2.315834,204
Benin,BEN,1999,214.735965,28.10456399,9.30769,2.315834,204
Benin,BEN,2000,212.733143,28.31386892,9.30769,2.315834,204
Benin,BEN,2001,208.2024145,27.73781903,9.30769,2.315834,204
Benin,BEN,2002,206.9325271,27.27325525,9.30769,2.315834,204
Benin,BEN,2003,202.5048493,26.58366078,9.30769,2.315834,204
Benin,BEN,2004,199.3745664,26.17279994,9.30769,2.315834,204
Benin,BEN,2005,195.2343272,26.11024841,9.30769,2.315834,204
Benin,BEN,2006,192.4619209,26.75556998,9.30769,2.315834,204
Benin,BEN,2007,187.2143003,26.8461345,9.30769,2.315834,204
Benin,BEN,2008,185.3466738,27.29357443,9.30769,2.315834,204
Benin,BEN,2009,183.3202332,27.80889978,9.30769,2.315834,204
Benin,BEN,2010,181.2675303,29.00945847,9.30769,2.315834,204
Benin,BEN,2011,178.1788099,30.7229986,9.30769,2.315834,204
Benin,BEN,2012,174.5897013,33.04994311,9.30769,2.315834,204
Benin,BEN,2013,169.7875787,35.27053992,9.30769,2.315834,204
Benin,BEN,2014,164.0971402,36.52905515,9.30769,2.315834,204
Benin,BEN,2015,161.902002,37.44175739,9.30769,2.315834,204
Benin,BEN,2016,157.9648917,36.29724163,9.30769,2.315834,204
Benin,BEN,2017,155.0629532,35.76466132,9.30769,2.315834,204
Benin,BEN,2018,148.9577812,36.39605207,9.30769,2.315834,204
Benin,BEN,2019,143.4844465,38.0050594,9.30769,2.315834,204
Bermuda,BMU,1990,10.58897053,27.2359484,32.321384,-64.75737,60
Bermuda,BMU,1991,9.530155256,26.11993368,32.321384,-64.75737,60
Bermuda,BMU,1992,8.462805903,24.6671076,32.321384,-64.75737,60
Bermuda,BMU,1993,7.776114921,24.25963977,32.321384,-64.75737,60
Bermuda,BMU,1994,7.020727726,23.48446856,32.321384,-64.75737,60
Bermuda,BMU,1995,6.161908458,22.01637933,32.321384,-64.75737,60
Bermuda,BMU,1996,5.690185858,21.49060277,32.321384,-64.75737,60
Bermuda,BMU,1997,4.914968929,19.34260349,32.321384,-64.75737,60
Bermuda,BMU,1998,4.342575534,17.62656816,32.321384,-64.75737,60
Bermuda,BMU,1999,3.90895289,16.2414916,32.321384,-64.75737,60
Bermuda,BMU,2000,3.532852955,15.17633468,32.321384,-64.75737,60
Bermuda,BMU,2001,3.09359728,13.99635498,32.321384,-64.75737,60
Bermuda,BMU,2002,2.750053884,13.1482166,32.321384,-64.75737,60
Bermuda,BMU,2003,2.44442009,12.31614406,32.321384,-64.75737,60
Bermuda,BMU,2004,2.186036596,11.55764372,32.321384,-64.75737,60
Bermuda,BMU,2005,1.962390236,10.98998404,32.321384,-64.75737,60
Bermuda,BMU,2006,1.748256265,10.38934288,32.321384,-64.75737,60
Bermuda,BMU,2007,1.529666456,9.666524769,32.321384,-64.75737,60
Bermuda,BMU,2008,1.337134259,8.930729248,32.321384,-64.75737,60
Bermuda,BMU,2009,1.176282125,8.425165333,32.321384,-64.75737,60
Bermuda,BMU,2010,1.04338793,7.905924604,32.321384,-64.75737,60
Bermuda,BMU,2011,0.952766123,7.698769243,32.321384,-64.75737,60
Bermuda,BMU,2012,0.870509607,7.355021567,32.321384,-64.75737,60
Bermuda,BMU,2013,0.80813284,7.214072197,32.321384,-64.75737,60
Bermuda,BMU,2014,0.751934642,7.082037295,32.321384,-64.75737,60
Bermuda,BMU,2015,0.703074865,7.066530893,32.321384,-64.75737,60
Bermuda,BMU,2016,0.665539643,7.161744101,32.321384,-64.75737,60
Bermuda,BMU,2017,0.634201245,7.267217238,32.321384,-64.75737,60
Bermuda,BMU,2018,0.593504362,7.011243317,32.321384,-64.75737,60
Bermuda,BMU,2019,0.545315294,6.739174439,32.321384,-64.75737,60
Bhutan,BTN,1990,225.902612,29.857346,27.514162,90.433601,64
Bhutan,BTN,1991,225.4226921,30.29899624,27.514162,90.433601,64
Bhutan,BTN,1992,220.76767,30.06265487,27.514162,90.433601,64
Bhutan,BTN,1993,215.9061913,30.76148668,27.514162,90.433601,64
Bhutan,BTN,1994,210.9800133,31.3679578,27.514162,90.433601,64
Bhutan,BTN,1995,206.3831803,32.66080289,27.514162,90.433601,64
Bhutan,BTN,1996,200.1375262,33.26313456,27.514162,90.433601,64
Bhutan,BTN,1997,196.493526,34.77770746,27.514162,90.433601,64
Bhutan,BTN,1998,191.689765,36.40416467,27.514162,90.433601,64
Bhutan,BTN,1999,183.0714656,37.87686512,27.514162,90.433601,64
Bhutan,BTN,2000,179.1571651,39.26361371,27.514162,90.433601,64
Bhutan,BTN,2001,171.4049019,39.47534171,27.514162,90.433601,64
Bhutan,BTN,2002,162.5560934,40.72374344,27.514162,90.433601,64
Bhutan,BTN,2003,155.1265688,43.45197291,27.514162,90.433601,64
Bhutan,BTN,2004,146.5878225,46.12416175,27.514162,90.433601,64
Bhutan,BTN,2005,138.2490624,47.87052168,27.514162,90.433601,64
Bhutan,BTN,2006,128.9915065,49.94267587,27.514162,90.433601,64
Bhutan,BTN,2007,121.5416803,53.92065724,27.514162,90.433601,64
Bhutan,BTN,2008,113.3151127,56.53139863,27.514162,90.433601,64
Bhutan,BTN,2009,106.0470999,57.80460092,27.514162,90.433601,64
Bhutan,BTN,2010,99.90670583,58.81086625,27.514162,90.433601,64
Bhutan,BTN,2011,94.88393444,61.8124958,27.514162,90.433601,64
Bhutan,BTN,2012,90.2816919,65.49278118,27.514162,90.433601,64
Bhutan,BTN,2013,86.30758939,67.71567642,27.514162,90.433601,64
Bhutan,BTN,2014,82.8248112,67.93550277,27.514162,90.433601,64
Bhutan,BTN,2015,80.01282323,68.07321358,27.514162,90.433601,64
Bhutan,BTN,2016,77.66151309,67.83724337,27.514162,90.433601,64
Bhutan,BTN,2017,75.45563727,67.42844798,27.514162,90.433601,64
Bhutan,BTN,2018,72.95124364,66.54597392,27.514162,90.433601,64
Bhutan,BTN,2019,70.04096991,68.16329086,27.514162,90.433601,64
Bolivia,BOL,1990,112.0902224,69.0640297,-16.290154,-63.588653,68
Bolivia,BOL,1991,105.4339869,69.17456324,-16.290154,-63.588653,68
Bolivia,BOL,1992,99.40991502,68.830403,-16.290154,-63.588653,68
Bolivia,BOL,1993,94.02488071,68.10927528,-16.290154,-63.588653,68
Bolivia,BOL,1994,88.41364723,66.67883577,-16.290154,-63.588653,68
Bolivia,BOL,1995,83.99724818,65.28212453,-16.290154,-63.588653,68
Bolivia,BOL,1996,79.54797953,62.1346032,-16.290154,-63.588653,68
Bolivia,BOL,1997,76.62434639,58.56683231,-16.290154,-63.588653,68
Bolivia,BOL,1998,73.01004741,54.22096963,-16.290154,-63.588653,68
Bolivia,BOL,1999,69.71633451,50.54067695,-16.290154,-63.588653,68
Bolivia,BOL,2000,66.44071646,48.13064435,-16.290154,-63.588653,68
Bolivia,BOL,2001,62.85558372,46.6190975,-16.290154,-63.588653,68
Bolivia,BOL,2002,59.74028368,45.73586028,-16.290154,-63.588653,68
Bolivia,BOL,2003,56.67817972,45.0536962,-16.290154,-63.588653,68
Bolivia,BOL,2004,53.81399578,44.47492025,-16.290154,-63.588653,68
Bolivia,BOL,2005,51.4975989,44.28512613,-16.290154,-63.588653,68
Bolivia,BOL,2006,49.41118331,44.7220992,-16.290154,-63.588653,68
Bolivia,BOL,2007,47.81952906,46.07167381,-16.290154,-63.588653,68
Bolivia,BOL,2008,46.21306568,47.20747089,-16.290154,-63.588653,68
Bolivia,BOL,2009,44.71616884,48.37903631,-16.290154,-63.588653,68
Bolivia,BOL,2010,43.36033944,48.90212808,-16.290154,-63.588653,68
Bolivia,BOL,2011,42.30490357,49.21363407,-16.290154,-63.588653,68
Bolivia,BOL,2012,41.33228579,49.21344108,-16.290154,-63.588653,68
Bolivia,BOL,2013,40.35431012,48.42865892,-16.290154,-63.588653,68
Bolivia,BOL,2014,39.08637142,47.83526196,-16.290154,-63.588653,68
Bolivia,BOL,2015,37.54725392,47.53731216,-16.290154,-63.588653,68
Bolivia,BOL,2016,34.59551972,48.16546749,-16.290154,-63.588653,68
Bolivia,BOL,2017,31.37493975,48.47733665,-16.290154,-63.588653,68
Bolivia,BOL,2018,29.31828898,48.98598305,-16.290154,-63.588653,68
Bolivia,BOL,2019,27.75903854,49.42458387,-16.290154,-63.588653,68
Bosnia and Herzegovina,BIH,1990,90.59530675,60.39682117,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1991,96.92661683,64.46036675,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1992,96.87411616,64.12336035,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1993,96.47749554,64.94002234,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1994,95.58698404,64.96457645,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1995,93.06626993,64.13217591,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1996,86.98865047,63.44028242,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1997,79.42509675,65.60356635,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1998,66.00792425,64.63016595,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,1999,57.04552842,66.09308495,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2000,51.96381239,68.16992416,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2001,51.89912614,73.17577178,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2002,50.44226632,76.9151932,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2003,47.35413898,77.88873259,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2004,44.37677759,77.74057425,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2005,42.28964538,79.23292004,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2006,38.9482476,77.3168284,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2007,37.81765063,79.79292461,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2008,33.61145924,74.97422588,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2009,31.37740189,73.79327066,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2010,29.28436828,72.28571873,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2011,28.07040715,72.58505511,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2012,26.2798697,71.1197527,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2013,25.13434713,70.9860736,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2014,24.25388648,70.92805539,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2015,23.97870788,71.85536486,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2016,22.76755282,68.10122285,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2017,21.90214395,65.22914669,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2018,21.13339189,65.18937351,43.915886,17.679076,70
Bosnia and Herzegovina,BIH,2019,20.10527349,64.64710238,43.915886,17.679076,70
Botswana,BWA,1990,165.059865,39.38699988,-22.328474,24.684866,72
Botswana,BWA,1991,160.8837335,41.72085203,-22.328474,24.684866,72
Botswana,BWA,1992,158.0928641,44.17727985,-22.328474,24.684866,72
Botswana,BWA,1993,155.5368865,46.98278942,-22.328474,24.684866,72
Botswana,BWA,1994,154.1935921,50.27103278,-22.328474,24.684866,72
Botswana,BWA,1995,152.5621916,53.95018815,-22.328474,24.684866,72
Botswana,BWA,1996,149.1944778,57.28132038,-22.328474,24.684866,72
Botswana,BWA,1997,145.0419726,60.35243581,-22.328474,24.684866,72
Botswana,BWA,1998,142.6012382,63.87585052,-22.328474,24.684866,72
Botswana,BWA,1999,139.6284175,67.29532803,-22.328474,24.684866,72
Botswana,BWA,2000,137.7074531,70.70582726,-22.328474,24.684866,72
Botswana,BWA,2001,134.4466887,73.7714487,-22.328474,24.684866,72
Botswana,BWA,2002,130.238066,75.96931297,-22.328474,24.684866,72
Botswana,BWA,2003,123.5587324,77.08663564,-22.328474,24.684866,72
Botswana,BWA,2004,114.7910454,77.50713392,-22.328474,24.684866,72
Botswana,BWA,2005,105.3799859,77.14562437,-22.328474,24.684866,72
Botswana,BWA,2006,98.06462917,78.56550689,-22.328474,24.684866,72
Botswana,BWA,2007,90.29682013,77.89302595,-22.328474,24.684866,72
Botswana,BWA,2008,85.55753718,79.17707076,-22.328474,24.684866,72
Botswana,BWA,2009,80.66440995,79.71805158,-22.328474,24.684866,72
Botswana,BWA,2010,77.04834255,80.68004644,-22.328474,24.684866,72
Botswana,BWA,2011,73.67550597,81.33582065,-22.328474,24.684866,72
Botswana,BWA,2012,69.88463925,81.28668227,-22.328474,24.684866,72
Botswana,BWA,2013,66.72406732,81.12226209,-22.328474,24.684866,72
Botswana,BWA,2014,63.85910758,80.40729326,-22.328474,24.684866,72
Botswana,BWA,2015,61.19148445,79.35805683,-22.328474,24.684866,72
Botswana,BWA,2016,58.47733914,77.25747217,-22.328474,24.684866,72
Botswana,BWA,2017,56.37616413,76.00337699,-22.328474,24.684866,72
Botswana,BWA,2018,53.56255587,75.57422409,-22.328474,24.684866,72
Botswana,BWA,2019,50.05638446,75.8293091,-22.328474,24.684866,72
Brazil,BRA,1990,62.25207406,35.35654128,-14.235004,-51.92528,76
Brazil,BRA,1991,56.36920651,34.17803594,-14.235004,-51.92528,76
Brazil,BRA,1992,51.88713302,34.04460984,-14.235004,-51.92528,76
Brazil,BRA,1993,48.33284786,34.84879955,-14.235004,-51.92528,76
Brazil,BRA,1994,43.87201102,34.58916684,-14.235004,-51.92528,76
Brazil,BRA,1995,40.04843953,34.08452308,-14.235004,-51.92528,76
Brazil,BRA,1996,36.82390778,33.88929804,-14.235004,-51.92528,76
Brazil,BRA,1997,33.73924163,32.98569117,-14.235004,-51.92528,76
Brazil,BRA,1998,31.51313284,32.8717419,-14.235004,-51.92528,76
Brazil,BRA,1999,29.11985452,32.37436073,-14.235004,-51.92528,76
Brazil,BRA,2000,26.98972618,31.55198667,-14.235004,-51.92528,76
Brazil,BRA,2001,25.32530581,31.15365679,-14.235004,-51.92528,76
Brazil,BRA,2002,23.77461583,30.91286913,-14.235004,-51.92528,76
Brazil,BRA,2003,22.26738374,30.66404048,-14.235004,-51.92528,76
Brazil,BRA,2004,20.77717554,30.08585338,-14.235004,-51.92528,76
Brazil,BRA,2005,19.08957499,28.92251546,-14.235004,-51.92528,76
Brazil,BRA,2006,17.70394564,28.74528969,-14.235004,-51.92528,76
Brazil,BRA,2007,16.4416337,28.33221348,-14.235004,-51.92528,76
Brazil,BRA,2008,15.2611926,27.85985232,-14.235004,-51.92528,76
Brazil,BRA,2009,14.17399182,27.54487567,-14.235004,-51.92528,76
Brazil,BRA,2010,13.18550539,27.1758332,-14.235004,-51.92528,76
Brazil,BRA,2011,12.29670828,26.47548333,-14.235004,-51.92528,76
Brazil,BRA,2012,11.22414584,24.8542738,-14.235004,-51.92528,76
Brazil,BRA,2013,10.23372877,23.42263378,-14.235004,-51.92528,76
Brazil,BRA,2014,9.330938379,22.01039322,-14.235004,-51.92528,76
Brazil,BRA,2015,8.620754415,21.31601091,-14.235004,-51.92528,76
Brazil,BRA,2016,8.019037707,21.46030047,-14.235004,-51.92528,76
Brazil,BRA,2017,7.357707392,20.7603274,-14.235004,-51.92528,76
Brazil,BRA,2018,6.816780969,20.9111448,-14.235004,-51.92528,76
Brazil,BRA,2019,6.298325736,20.93499949,-14.235004,-51.92528,76
Brunei,BRN,1990,13.69308897,32.28638769,4.535277,114.727669,96
Brunei,BRN,1991,11.70572695,29.69774698,4.535277,114.727669,96
Brunei,BRN,1992,9.983011009,27.5050362,4.535277,114.727669,96
Brunei,BRN,1993,8.460168846,25.74437024,4.535277,114.727669,96
Brunei,BRN,1994,6.968755547,23.04478511,4.535277,114.727669,96
Brunei,BRN,1995,5.878883454,21.38437775,4.535277,114.727669,96
Brunei,BRN,1996,4.94489515,20.12050359,4.535277,114.727669,96
Brunei,BRN,1997,4.461297219,21.2884982,4.535277,114.727669,96
Brunei,BRN,1998,3.862483099,20.87653005,4.535277,114.727669,96
Brunei,BRN,1999,3.313411234,19.2283741,4.535277,114.727669,96
Brunei,BRN,2000,2.846224111,18.12297758,4.535277,114.727669,96
Brunei,BRN,2001,2.383954339,17.65121623,4.535277,114.727669,96
Brunei,BRN,2002,2.030890601,17.67134123,4.535277,114.727669,96
Brunei,BRN,2003,1.74929688,18.28207061,4.535277,114.727669,96
Brunei,BRN,2004,1.489629123,18.03323406,4.535277,114.727669,96
Brunei,BRN,2005,1.291709333,18.35772452,4.535277,114.727669,96
Brunei,BRN,2006,1.100892299,17.73889029,4.535277,114.727669,96
Brunei,BRN,2007,0.90860238,16.36268601,4.535277,114.727669,96
Brunei,BRN,2008,0.743443409,14.9488777,4.535277,114.727669,96
Brunei,BRN,2009,0.649918706,14.34618768,4.535277,114.727669,96
Brunei,BRN,2010,0.592172554,13.9696674,4.535277,114.727669,96
Brunei,BRN,2011,0.562486763,14.52436204,4.535277,114.727669,96
Brunei,BRN,2012,0.542666949,16.1616558,4.535277,114.727669,96
Brunei,BRN,2013,0.530587768,18.29364073,4.535277,114.727669,96
Brunei,BRN,2014,0.512793535,19.90839332,4.535277,114.727669,96
Brunei,BRN,2015,0.488321648,20.33435523,4.535277,114.727669,96
Brunei,BRN,2016,0.433223343,18.55633493,4.535277,114.727669,96
Brunei,BRN,2017,0.37796448,16.65321805,4.535277,114.727669,96
Brunei,BRN,2018,0.349375796,17.02912816,4.535277,114.727669,96
Brunei,BRN,2019,0.328817643,17.83225718,4.535277,114.727669,96
Bulgaria,BGR,1990,41.52978785,112.7522985,42.733883,25.48583,100
Bulgaria,BGR,1991,37.9653904,110.3088381,42.733883,25.48583,100
Bulgaria,BGR,1992,36.52970272,113.8646611,42.733883,25.48583,100
Bulgaria,BGR,1993,36.53071615,121.6508718,42.733883,25.48583,100
Bulgaria,BGR,1994,35.84829,125.8249677,42.733883,25.48583,100
Bulgaria,BGR,1995,34.50642218,125.8764792,42.733883,25.48583,100
Bulgaria,BGR,1996,33.70414727,125.5596824,42.733883,25.48583,100
Bulgaria,BGR,1997,33.86261106,128.3209242,42.733883,25.48583,100
Bulgaria,BGR,1998,31.87288736,122.5352465,42.733883,25.48583,100
Bulgaria,BGR,1999,29.91616616,115.7556864,42.733883,25.48583,100
Bulgaria,BGR,2000,28.9799851,113.1837361,42.733883,25.48583,100
Bulgaria,BGR,2001,27.66799566,109.3440579,42.733883,25.48583,100
Bulgaria,BGR,2002,26.55866186,106.0029917,42.733883,25.48583,100
Bulgaria,BGR,2003,25.22544365,101.5666122,42.733883,25.48583,100
Bulgaria,BGR,2004,23.95398742,96.90597699,42.733883,25.48583,100
Bulgaria,BGR,2005,23.09887046,94.02953234,42.733883,25.48583,100
Bulgaria,BGR,2006,22.1587408,91.77862991,42.733883,25.48583,100
Bulgaria,BGR,2007,20.76997249,87.96515804,42.733883,25.48583,100
Bulgaria,BGR,2008,19.41350913,84.45814387,42.733883,25.48583,100
Bulgaria,BGR,2009,18.31339307,81.56701456,42.733883,25.48583,100
Bulgaria,BGR,2010,17.50081478,79.27801824,42.733883,25.48583,100
Bulgaria,BGR,2011,16.62209036,76.27520004,42.733883,25.48583,100
Bulgaria,BGR,2012,15.6182917,72.28214595,42.733883,25.48583,100
Bulgaria,BGR,2013,14.74518974,68.66582371,42.733883,25.48583,100
Bulgaria,BGR,2014,14.71127251,68.5415039,42.733883,25.48583,100
Bulgaria,BGR,2015,14.15713785,66.36030093,42.733883,25.48583,100
Bulgaria,BGR,2016,13.6409782,64.86085039,42.733883,25.48583,100
Bulgaria,BGR,2017,13.1614085,63.78526199,42.733883,25.48583,100
Bulgaria,BGR,2018,12.92671336,64.16794567,42.733883,25.48583,100
Bulgaria,BGR,2019,12.46774132,63.80244389,42.733883,25.48583,100
Burkina Faso,BFA,1990,240.6461972,15.92984526,12.238333,-1.561593,854
Burkina Faso,BFA,1991,235.7886664,15.67740912,12.238333,-1.561593,854
Burkina Faso,BFA,1992,233.024099,15.51696214,12.238333,-1.561593,854
Burkina Faso,BFA,1993,231.1139781,15.50859363,12.238333,-1.561593,854
Burkina Faso,BFA,1994,229.5167103,15.48018361,12.238333,-1.561593,854
Burkina Faso,BFA,1995,228.0978606,15.58247544,12.238333,-1.561593,854
Burkina Faso,BFA,1996,226.2070672,15.93355766,12.238333,-1.561593,854
Burkina Faso,BFA,1997,223.7231696,16.6089252,12.238333,-1.561593,854
Burkina Faso,BFA,1998,220.4213311,17.31021284,12.238333,-1.561593,854
Burkina Faso,BFA,1999,219.2148771,18.10296646,12.238333,-1.561593,854
Burkina Faso,BFA,2000,221.5270487,18.8784201,12.238333,-1.561593,854
Burkina Faso,BFA,2001,217.4381482,19.05690226,12.238333,-1.561593,854
Burkina Faso,BFA,2002,217.7531111,19.54838138,12.238333,-1.561593,854
Burkina Faso,BFA,2003,212.3781362,19.71373084,12.238333,-1.561593,854
Burkina Faso,BFA,2004,209.5688978,20.13871341,12.238333,-1.561593,854
Burkina Faso,BFA,2005,206.575001,20.63776926,12.238333,-1.561593,854
Burkina Faso,BFA,2006,204.0414435,21.21733739,12.238333,-1.561593,854
Burkina Faso,BFA,2007,198.113445,21.17366149,12.238333,-1.561593,854
Burkina Faso,BFA,2008,195.0636517,21.25250662,12.238333,-1.561593,854
Burkina Faso,BFA,2009,191.7754152,21.40382117,12.238333,-1.561593,854
Burkina Faso,BFA,2010,190.2822947,22.12917848,12.238333,-1.561593,854
Burkina Faso,BFA,2011,188.5008973,23.21292292,12.238333,-1.561593,854
Burkina Faso,BFA,2012,186.9332628,24.65081123,12.238333,-1.561593,854
Burkina Faso,BFA,2013,185.1160038,26.19919362,12.238333,-1.561593,854
Burkina Faso,BFA,2014,182.0850444,27.15347026,12.238333,-1.561593,854
Burkina Faso,BFA,2015,183.0620067,27.94156038,12.238333,-1.561593,854
Burkina Faso,BFA,2016,182.5775612,26.97021382,12.238333,-1.561593,854
Burkina Faso,BFA,2017,182.2590366,26.17697226,12.238333,-1.561593,854
Burkina Faso,BFA,2018,180.1595095,26.6667556,12.238333,-1.561593,854
Burkina Faso,BFA,2019,175.100291,27.13503403,12.238333,-1.561593,854
Burundi,BDI,1990,299.6503428,21.39348648,-3.373056,29.918886,108
Burundi,BDI,1991,300.242046,21.6715994,-3.373056,29.918886,108
Burundi,BDI,1992,299.666978,21.61378274,-3.373056,29.918886,108
Burundi,BDI,1993,297.1622838,21.35420504,-3.373056,29.918886,108
Burundi,BDI,1994,295.3151193,21.2379795,-3.373056,29.918886,108
Burundi,BDI,1995,297.5885032,21.72145241,-3.373056,29.918886,108
Burundi,BDI,1996,295.315441,21.73083885,-3.373056,29.918886,108
Burundi,BDI,1997,289.4684201,21.62069512,-3.373056,29.918886,108
Burundi,BDI,1998,284.1896709,21.07950982,-3.373056,29.918886,108
Burundi,BDI,1999,277.1919666,20.95497933,-3.373056,29.918886,108
Burundi,BDI,2000,271.1817171,20.08973848,-3.373056,29.918886,108
Burundi,BDI,2001,261.636129,19.34440855,-3.373056,29.918886,108
Burundi,BDI,2002,257.8992274,18.65301439,-3.373056,29.918886,108
Burundi,BDI,2003,254.2802964,18.28175062,-3.373056,29.918886,108
Burundi,BDI,2004,252.2743494,18.56397924,-3.373056,29.918886,108
Burundi,BDI,2005,248.9074011,18.95686807,-3.373056,29.918886,108
Burundi,BDI,2006,242.2468389,19.42937627,-3.373056,29.918886,108
Burundi,BDI,2007,234.5369076,18.75540617,-3.373056,29.918886,108
Burundi,BDI,2008,227.2069842,18.14267269,-3.373056,29.918886,108
Burundi,BDI,2009,221.466203,18.08154466,-3.373056,29.918886,108
Burundi,BDI,2010,218.9389025,18.81156568,-3.373056,29.918886,108
Burundi,BDI,2011,214.3159491,19.65010867,-3.373056,29.918886,108
Burundi,BDI,2012,210.0020667,20.63997641,-3.373056,29.918886,108
Burundi,BDI,2013,205.1128533,21.65753112,-3.373056,29.918886,108
Burundi,BDI,2014,200.4734721,22.1120019,-3.373056,29.918886,108
Burundi,BDI,2015,196.1310247,22.14917698,-3.373056,29.918886,108
Burundi,BDI,2016,191.2625383,21.10984165,-3.373056,29.918886,108
Burundi,BDI,2017,188.4994385,20.62813775,-3.373056,29.918886,108
Burundi,BDI,2018,188.4957381,21.62688551,-3.373056,29.918886,108
Burundi,BDI,2019,186.1511615,22.27031815,-3.373056,29.918886,108
Cambodia,KHM,1990,285.9820437,21.85282601,12.565679,104.990963,116
Cambodia,KHM,1991,281.7731365,21.87916799,12.565679,104.990963,116
Cambodia,KHM,1992,278.0132161,21.99751881,12.565679,104.990963,116
Cambodia,KHM,1993,275.2944624,22.35771928,12.565679,104.990963,116
Cambodia,KHM,1994,273.1349261,22.68634284,12.565679,104.990963,116
Cambodia,KHM,1995,270.2802925,23.08348505,12.565679,104.990963,116
Cambodia,KHM,1996,265.5070282,23.4178443,12.565679,104.990963,116
Cambodia,KHM,1997,260.0787834,24.08254146,12.565679,104.990963,116
Cambodia,KHM,1998,254.5258842,24.5542582,12.565679,104.990963,116
Cambodia,KHM,1999,248.4007323,25.15358606,12.565679,104.990963,116
Cambodia,KHM,2000,240.9611539,25.46828147,12.565679,104.990963,116
Cambodia,KHM,2001,233.6089572,26.4170492,12.565679,104.990963,116
Cambodia,KHM,2002,226.116809,27.49077002,12.565679,104.990963,116
Cambodia,KHM,2003,217.6742899,28.87089194,12.565679,104.990963,116
Cambodia,KHM,2004,209.6704088,29.84846671,12.565679,104.990963,116
Cambodia,KHM,2005,201.5824041,30.46008559,12.565679,104.990963,116
Cambodia,KHM,2006,193.4130913,31.22372983,12.565679,104.990963,116
Cambodia,KHM,2007,186.1996085,32.2096799,12.565679,104.990963,116
Cambodia,KHM,2008,179.3229201,33.16313702,12.565679,104.990963,116
Cambodia,KHM,2009,173.5316035,33.5967284,12.565679,104.990963,116
Cambodia,KHM,2010,169.3220396,34.39732175,12.565679,104.990963,116
Cambodia,KHM,2011,165.3313038,35.01953043,12.565679,104.990963,116
Cambodia,KHM,2012,161.1722127,35.22764442,12.565679,104.990963,116
Cambodia,KHM,2013,156.7469388,34.60601533,12.565679,104.990963,116
Cambodia,KHM,2014,152.7885649,33.88120509,12.565679,104.990963,116
Cambodia,KHM,2015,148.671492,33.50363441,12.565679,104.990963,116
Cambodia,KHM,2016,144.8531332,32.83513347,12.565679,104.990963,116
Cambodia,KHM,2017,141.1555714,32.29065873,12.565679,104.990963,116
Cambodia,KHM,2018,137.3108935,33.4003802,12.565679,104.990963,116
Cambodia,KHM,2019,133.1227054,34.83217875,12.565679,104.990963,116
Cameroon,CMR,1990,163.0028258,45.4613486,7.369722,12.354722,120
Cameroon,CMR,1991,161.5781951,45.9748446,7.369722,12.354722,120
Cameroon,CMR,1992,161.1381506,46.78216964,7.369722,12.354722,120
Cameroon,CMR,1993,160.8070153,47.767221,7.369722,12.354722,120
Cameroon,CMR,1994,159.48062,48.39042006,7.369722,12.354722,120
Cameroon,CMR,1995,158.4853267,49.31239466,7.369722,12.354722,120
Cameroon,CMR,1996,158.0935871,50.70750708,7.369722,12.354722,120
Cameroon,CMR,1997,158.5048878,52.9857022,7.369722,12.354722,120
Cameroon,CMR,1998,158.5500074,55.27478036,7.369722,12.354722,120
Cameroon,CMR,1999,157.6892455,56.9769081,7.369722,12.354722,120
Cameroon,CMR,2000,158.3920222,58.19200462,7.369722,12.354722,120
Cameroon,CMR,2001,156.2356078,57.9346463,7.369722,12.354722,120
Cameroon,CMR,2002,157.7188924,58.83837618,7.369722,12.354722,120
Cameroon,CMR,2003,155.8399579,58.75533979,7.369722,12.354722,120
Cameroon,CMR,2004,153.669871,58.76749645,7.369722,12.354722,120
Cameroon,CMR,2005,151.6248214,59.34127505,7.369722,12.354722,120
Cameroon,CMR,2006,149.598855,60.60851577,7.369722,12.354722,120
Cameroon,CMR,2007,144.3458268,60.64597913,7.369722,12.354722,120
Cameroon,CMR,2008,140.617079,61.39480989,7.369722,12.354722,120
Cameroon,CMR,2009,136.5029446,62.47580254,7.369722,12.354722,120
Cameroon,CMR,2010,132.4104622,64.16062343,7.369722,12.354722,120
Cameroon,CMR,2011,127.5964384,66.90394127,7.369722,12.354722,120
Cameroon,CMR,2012,122.0861284,70.74550784,7.369722,12.354722,120
Cameroon,CMR,2013,116.083513,74.6621634,7.369722,12.354722,120
Cameroon,CMR,2014,109.717615,76.87890893,7.369722,12.354722,120
Cameroon,CMR,2015,104.760948,77.55557457,7.369722,12.354722,120
Cameroon,CMR,2016,99.92551164,75.18438894,7.369722,12.354722,120
Cameroon,CMR,2017,95.67856672,73.43332125,7.369722,12.354722,120
Cameroon,CMR,2018,90.95446404,74.5714082,7.369722,12.354722,120
Cameroon,CMR,2019,84.94650458,77.18055803,7.369722,12.354722,120
Canada,CAN,1990,0.284440788,19.49027435,56.130366,-106.346771,124
Canada,CAN,1991,0.278567428,18.86149216,56.130366,-106.346771,124
Canada,CAN,1992,0.273388097,18.38007467,56.130366,-106.346771,124
Canada,CAN,1993,0.272023971,18.15464801,56.130366,-106.346771,124
Canada,CAN,1994,0.267315761,17.84812054,56.130366,-106.346771,124
Canada,CAN,1995,0.262496652,17.56613535,56.130366,-106.346771,124
Canada,CAN,1996,0.252025513,16.95191573,56.130366,-106.346771,124
Canada,CAN,1997,0.235928141,16.44429867,56.130366,-106.346771,124
Canada,CAN,1998,0.216114488,15.94293145,56.130366,-106.346771,124
Canada,CAN,1999,0.193778333,15.17778951,56.130366,-106.346771,124
Canada,CAN,2000,0.171200999,14.42277013,56.130366,-106.346771,124
Canada,CAN,2001,0.148904168,13.85896884,56.130366,-106.346771,124
Canada,CAN,2002,0.124732588,13.6608368,56.130366,-106.346771,124
Canada,CAN,2003,0.100004032,13.07416545,56.130366,-106.346771,124
Canada,CAN,2004,0.078056717,12.53694634,56.130366,-106.346771,124
Canada,CAN,2005,0.062256035,11.96236178,56.130366,-106.346771,124
Canada,CAN,2006,0.050433432,11.27111831,56.130366,-106.346771,124
Canada,CAN,2007,0.040938449,10.51286486,56.130366,-106.346771,124
Canada,CAN,2008,0.03292481,9.629642774,56.130366,-106.346771,124
Canada,CAN,2009,0.026604639,8.80626448,56.130366,-106.346771,124
Canada,CAN,2010,0.02231817,8.100770698,56.130366,-106.346771,124
Canada,CAN,2011,0.019473289,7.652820476,56.130366,-106.346771,124
Canada,CAN,2012,0.017406823,7.233758801,56.130366,-106.346771,124
Canada,CAN,2013,0.015766268,6.876954527,56.130366,-106.346771,124
Canada,CAN,2014,0.014580099,6.625003799,56.130366,-106.346771,124
Canada,CAN,2015,0.013555618,6.418630604,56.130366,-106.346771,124
Canada,CAN,2016,0.012966584,6.353540899,56.130366,-106.346771,124
Canada,CAN,2017,0.012426876,6.177589752,56.130366,-106.346771,124
Canada,CAN,2018,0.012150394,6.353642143,56.130366,-106.346771,124
Canada,CAN,2019,0.011579083,6.167969646,56.130366,-106.346771,124
Cape Verde,CPV,1990,107.3421219,23.6740088,16.002082,-24.013197,132
Cape Verde,CPV,1991,104.835143,23.92576512,16.002082,-24.013197,132
Cape Verde,CPV,1992,101.859629,24.44177272,16.002082,-24.013197,132
Cape Verde,CPV,1993,100.1402102,25.49130735,16.002082,-24.013197,132
Cape Verde,CPV,1994,97.62190118,26.49423491,16.002082,-24.013197,132
Cape Verde,CPV,1995,95.07566589,27.64630374,16.002082,-24.013197,132
Cape Verde,CPV,1996,93.32277539,29.85148106,16.002082,-24.013197,132
Cape Verde,CPV,1997,91.51892919,33.08604925,16.002082,-24.013197,132
Cape Verde,CPV,1998,86.00303287,35.02511951,16.002082,-24.013197,132
Cape Verde,CPV,1999,81.63480017,37.22345577,16.002082,-24.013197,132
Cape Verde,CPV,2000,76.66482183,38.16383411,16.002082,-24.013197,132
Cape Verde,CPV,2001,72.49459959,38.87391695,16.002082,-24.013197,132
Cape Verde,CPV,2002,68.64753459,39.68026499,16.002082,-24.013197,132
Cape Verde,CPV,2003,64.63035618,40.27703788,16.002082,-24.013197,132
Cape Verde,CPV,2004,60.91473441,40.74671156,16.002082,-24.013197,132
Cape Verde,CPV,2005,57.38632091,40.92854981,16.002082,-24.013197,132
Cape Verde,CPV,2006,51.17428564,38.20793365,16.002082,-24.013197,132
Cape Verde,CPV,2007,47.03182004,36.931487,16.002082,-24.013197,132
Cape Verde,CPV,2008,43.90677773,36.43839847,16.002082,-24.013197,132
Cape Verde,CPV,2009,40.98826892,36.20594174,16.002082,-24.013197,132
Cape Verde,CPV,2010,38.08136452,36.21145457,16.002082,-24.013197,132
Cape Verde,CPV,2011,36.01852747,39.13340119,16.002082,-24.013197,132
Cape Verde,CPV,2012,33.39490108,44.33721274,16.002082,-24.013197,132
Cape Verde,CPV,2013,30.38957219,50.05924666,16.002082,-24.013197,132
Cape Verde,CPV,2014,28.08878535,55.61495973,16.002082,-24.013197,132
Cape Verde,CPV,2015,26.45549961,59.59102862,16.002082,-24.013197,132
Cape Verde,CPV,2016,25.75422872,62.68908269,16.002082,-24.013197,132
Cape Verde,CPV,2017,24.16580699,63.89049292,16.002082,-24.013197,132
Cape Verde,CPV,2018,25.71330249,77.10054794,16.002082,-24.013197,132
Cape Verde,CPV,2019,23.60247128,76.89977866,16.002082,-24.013197,132
Central African Republic,CAF,1990,326.1946843,33.4955739,6.611111,20.939444,140
Central African Republic,CAF,1991,323.3418299,33.88006213,6.611111,20.939444,140
Central African Republic,CAF,1992,316.745703,33.42274163,6.611111,20.939444,140
Central African Republic,CAF,1993,315.7843927,33.42505882,6.611111,20.939444,140
Central African Republic,CAF,1994,314.3393694,33.44296428,6.611111,20.939444,140
Central African Republic,CAF,1995,312.7803009,34.5960857,6.611111,20.939444,140
Central African Republic,CAF,1996,314.547648,35.11520693,6.611111,20.939444,140
Central African Republic,CAF,1997,312.1374707,35.22527549,6.611111,20.939444,140
Central African Republic,CAF,1998,310.7506964,34.72097786,6.611111,20.939444,140
Central African Republic,CAF,1999,309.5687361,34.7044049,6.611111,20.939444,140
Central African Republic,CAF,2000,305.9646934,33.29016304,6.611111,20.939444,140
Central African Republic,CAF,2001,303.730554,32.44794409,6.611111,20.939444,140
Central African Republic,CAF,2002,302.4963854,31.80003697,6.611111,20.939444,140
Central African Republic,CAF,2003,300.4732646,31.97495866,6.611111,20.939444,140
Central African Republic,CAF,2004,298.6262497,32.02345234,6.611111,20.939444,140
Central African Republic,CAF,2005,296.2400455,33.35857238,6.611111,20.939444,140
Central African Republic,CAF,2006,295.3077837,34.83526162,6.611111,20.939444,140
Central African Republic,CAF,2007,292.3215296,35.64540346,6.611111,20.939444,140
Central African Republic,CAF,2008,288.366663,34.94165368,6.611111,20.939444,140
Central African Republic,CAF,2009,285.5198009,34.94618193,6.611111,20.939444,140
Central African Republic,CAF,2010,284.4367411,35.85421024,6.611111,20.939444,140
Central African Republic,CAF,2011,281.2561356,36.91683507,6.611111,20.939444,140
Central African Republic,CAF,2012,276.731848,37.72482067,6.611111,20.939444,140
Central African Republic,CAF,2013,274.7550941,39.36470716,6.611111,20.939444,140
Central African Republic,CAF,2014,270.0640723,39.86944151,6.611111,20.939444,140
Central African Republic,CAF,2015,266.2026941,40.69688956,6.611111,20.939444,140
Central African Republic,CAF,2016,263.1836682,40.20416595,6.611111,20.939444,140
Central African Republic,CAF,2017,261.1131702,40.29089015,6.611111,20.939444,140
Central African Republic,CAF,2018,257.0428747,39.45284115,6.611111,20.939444,140
Central African Republic,CAF,2019,251.2403818,40.71187778,6.611111,20.939444,140
Chad,TCD,1990,263.0740314,18.44869885,15.454166,18.732207,148
Chad,TCD,1991,259.8636918,18.17408449,15.454166,18.732207,148
Chad,TCD,1992,259.6429665,18.02495522,15.454166,18.732207,148
Chad,TCD,1993,260.5562912,18.10807997,15.454166,18.732207,148
Chad,TCD,1994,260.2137479,18.14803699,15.454166,18.732207,148
Chad,TCD,1995,260.4065697,18.36930068,15.454166,18.732207,148
Chad,TCD,1996,263.9318335,19.02289666,15.454166,18.732207,148
Chad,TCD,1997,264.9360789,19.84390166,15.454166,18.732207,148
Chad,TCD,1998,264.5842759,20.45378613,15.454166,18.732207,148
Chad,TCD,1999,263.4983852,21.06708422,15.454166,18.732207,148
Chad,TCD,2000,262.7403569,21.11271227,15.454166,18.732207,148
Chad,TCD,2001,261.8849116,21.31864786,15.454166,18.732207,148
Chad,TCD,2002,262.4625107,21.61614056,15.454166,18.732207,148
Chad,TCD,2003,261.6866653,22.08563398,15.454166,18.732207,148
Chad,TCD,2004,257.8767936,22.49643105,15.454166,18.732207,148
Chad,TCD,2005,251.9798591,22.88551464,15.454166,18.732207,148
Chad,TCD,2006,249.0192613,23.67036878,15.454166,18.732207,148
Chad,TCD,2007,246.3668123,24.02567606,15.454166,18.732207,148
Chad,TCD,2008,243.954112,23.95448633,15.454166,18.732207,148
Chad,TCD,2009,240.6424196,24.10059193,15.454166,18.732207,148
Chad,TCD,2010,237.1586009,24.60316398,15.454166,18.732207,148
Chad,TCD,2011,232.8989824,25.82567719,15.454166,18.732207,148
Chad,TCD,2012,227.7214333,27.30884273,15.454166,18.732207,148
Chad,TCD,2013,221.7801219,29.07556492,15.454166,18.732207,148
Chad,TCD,2014,215.0473001,30.17030253,15.454166,18.732207,148
Chad,TCD,2015,211.1536464,30.781854,15.454166,18.732207,148
Chad,TCD,2016,206.7832548,30.31212045,15.454166,18.732207,148
Chad,TCD,2017,203.4551051,30.14547774,15.454166,18.732207,148
Chad,TCD,2018,200.2328694,30.62947548,15.454166,18.732207,148
Chad,TCD,2019,195.5502333,31.1791315,15.454166,18.732207,148
Chile,CHL,1990,22.3530585,41.46980568,-35.675147,-71.542969,152
Chile,CHL,1991,19.92427097,39.1698649,-35.675147,-71.542969,152
Chile,CHL,1992,17.97767345,37.61124853,-35.675147,-71.542969,152
Chile,CHL,1993,16.51650009,37.09190757,-35.675147,-71.542969,152
Chile,CHL,1994,14.97060653,36.2658983,-35.675147,-71.542969,152
Chile,CHL,1995,13.7983616,36.20028781,-35.675147,-71.542969,152
Chile,CHL,1996,12.5454562,36.05852854,-35.675147,-71.542969,152
Chile,CHL,1997,11.00622405,35.06918265,-35.675147,-71.542969,152
Chile,CHL,1998,9.870044863,35.20972242,-35.675147,-71.542969,152
Chile,CHL,1999,8.829639513,35.18002741,-35.675147,-71.542969,152
Chile,CHL,2000,7.620350921,33.40143651,-35.675147,-71.542969,152
Chile,CHL,2001,6.923407836,33.00377967,-35.675147,-71.542969,152
Chile,CHL,2002,6.14251441,31.71378589,-35.675147,-71.542969,152
Chile,CHL,2003,5.638383279,31.34951123,-35.675147,-71.542969,152
Chile,CHL,2004,5.148957557,30.69618449,-35.675147,-71.542969,152
Chile,CHL,2005,4.62458382,29.53620127,-35.675147,-71.542969,152
Chile,CHL,2006,4.190888111,28.63805751,-35.675147,-71.542969,152
Chile,CHL,2007,3.875930643,28.28650381,-35.675147,-71.542969,152
Chile,CHL,2008,3.4865589,27.15529251,-35.675147,-71.542969,152
Chile,CHL,2009,3.297809366,27.42586007,-35.675147,-71.542969,152
Chile,CHL,2010,3.092626774,27.61204211,-35.675147,-71.542969,152
Chile,CHL,2011,2.795014252,27.25650842,-35.675147,-71.542969,152
Chile,CHL,2012,2.524530701,27.28460231,-35.675147,-71.542969,152
Chile,CHL,2013,2.279460699,27.52423877,-35.675147,-71.542969,152
Chile,CHL,2014,2.041321765,27.38223361,-35.675147,-71.542969,152
Chile,CHL,2015,1.859447752,27.09876081,-35.675147,-71.542969,152
Chile,CHL,2016,1.691495192,25.48145258,-35.675147,-71.542969,152
Chile,CHL,2017,1.609596355,24.71901198,-35.675147,-71.542969,152
Chile,CHL,2018,1.50743755,24.72131619,-35.675147,-71.542969,152
Chile,CHL,2019,1.403711714,25.15657005,-35.675147,-71.542969,152
China,CHN,1990,195.5605289,95.99842699,35.86166,104.195397,156
China,CHN,1991,187.980299,96.86915671,35.86166,104.195397,156
China,CHN,1992,180.5190497,98.95906865,35.86166,104.195397,156
China,CHN,1993,172.6411213,100.4825136,35.86166,104.195397,156
China,CHN,1994,163.4184221,101.9414633,35.86166,104.195397,156
China,CHN,1995,153.9108824,102.6575607,35.86166,104.195397,156
China,CHN,1996,144.877818,104.1052688,35.86166,104.195397,156
China,CHN,1997,134.5850428,105.5025326,35.86166,104.195397,156
China,CHN,1998,124.7279983,105.7852587,35.86166,104.195397,156
China,CHN,1999,117.4120323,108.4490447,35.86166,104.195397,156
China,CHN,2000,111.553853,110.0383778,35.86166,104.195397,156
China,CHN,2001,104.8984647,110.5572045,35.86166,104.195397,156
China,CHN,2002,98.87575056,110.695169,35.86166,104.195397,156
China,CHN,2003,92.91812578,111.145812,35.86166,104.195397,156
China,CHN,2004,87.89253124,112.9710542,35.86166,104.195397,156
China,CHN,2005,81.11455848,111.8817096,35.86166,104.195397,156
China,CHN,2006,71.97797104,108.6895996,35.86166,104.195397,156
China,CHN,2007,64.25544343,107.3145881,35.86166,104.195397,156
China,CHN,2008,58.32883487,108.7190492,35.86166,104.195397,156
China,CHN,2009,53.30476905,109.0061928,35.86166,104.195397,156
China,CHN,2010,49.09900707,109.6791119,35.86166,104.195397,156
China,CHN,2011,44.7632834,108.0162918,35.86166,104.195397,156
China,CHN,2012,40.11006807,104.7642157,35.86166,104.195397,156
China,CHN,2013,36.28886105,102.0051822,35.86166,104.195397,156
China,CHN,2014,33.01188377,99.43949379,35.86166,104.195397,156
China,CHN,2015,30.05552738,97.07136587,35.86166,104.195397,156
China,CHN,2016,27.95381074,94.58424656,35.86166,104.195397,156
China,CHN,2017,25.8470569,91.06352375,35.86166,104.195397,156
China,CHN,2018,23.39753177,87.77853844,35.86166,104.195397,156
China,CHN,2019,20.72933189,87.19569323,35.86166,104.195397,156
Colombia,COL,1990,45.15686279,39.72435147,4.570868,-74.297333,170
Colombia,COL,1991,44.50727843,40.82461563,4.570868,-74.297333,170
Colombia,COL,1992,42.50080949,40.71292478,4.570868,-74.297333,170
Colombia,COL,1993,39.95618729,40.10658315,4.570868,-74.297333,170
Colombia,COL,1994,37.60392935,39.8025549,4.570868,-74.297333,170
Colombia,COL,1995,35.08278338,39.36859374,4.570868,-74.297333,170
Colombia,COL,1996,32.97484547,39.88507579,4.570868,-74.297333,170
Colombia,COL,1997,28.96151736,38.28063082,4.570868,-74.297333,170
Colombia,COL,1998,25.9467736,37.6527115,4.570868,-74.297333,170
Colombia,COL,1999,24.23925664,38.3218612,4.570868,-74.297333,170
Colombia,COL,2000,22.5101049,37.57417016,4.570868,-74.297333,170
Colombia,COL,2001,21.35097665,36.71991108,4.570868,-74.297333,170
Colombia,COL,2002,21.8711625,38.32576281,4.570868,-74.297333,170
Colombia,COL,2003,20.09123512,34.68174361,4.570868,-74.297333,170
Colombia,COL,2004,19.02763933,32.63538776,4.570868,-74.297333,170
Colombia,COL,2005,17.46264084,30.33973032,4.570868,-74.297333,170
Colombia,COL,2006,16.50348366,30.47009574,4.570868,-74.297333,170
Colombia,COL,2007,14.83600878,29.88621485,4.570868,-74.297333,170
Colombia,COL,2008,13.55293314,30.33499062,4.570868,-74.297333,170
Colombia,COL,2009,12.51079041,31.19670111,4.570868,-74.297333,170
Colombia,COL,2010,11.25413902,30.51416644,4.570868,-74.297333,170
Colombia,COL,2011,9.843330271,28.70726553,4.570868,-74.297333,170
Colombia,COL,2012,8.885881349,28.06459519,4.570868,-74.297333,170
Colombia,COL,2013,7.985846835,27.11159901,4.570868,-74.297333,170
Colombia,COL,2014,7.196285118,26.12930111,4.570868,-74.297333,170
Colombia,COL,2015,6.611367983,25.8485893,4.570868,-74.297333,170
Colombia,COL,2016,6.003926979,25.26907182,4.570868,-74.297333,170
Colombia,COL,2017,5.45307442,24.58057275,4.570868,-74.297333,170
Colombia,COL,2018,5.019577276,24.78439892,4.570868,-74.297333,170
Colombia,COL,2019,4.586016001,24.83174351,4.570868,-74.297333,170
Comoros,COM,1990,227.1374931,11.73159214,-11.875001,43.872219,174
Comoros,COM,1991,222.2953887,12.06686513,-11.875001,43.872219,174
Comoros,COM,1992,222.8548334,12.68747555,-11.875001,43.872219,174
Comoros,COM,1993,218.7373433,13.0542396,-11.875001,43.872219,174
Comoros,COM,1994,217.568366,13.59970391,-11.875001,43.872219,174
Comoros,COM,1995,214.400188,14.00167844,-11.875001,43.872219,174
Comoros,COM,1996,210.6783926,14.354256,-11.875001,43.872219,174
Comoros,COM,1997,205.7536702,14.61595505,-11.875001,43.872219,174
Comoros,COM,1998,197.1976944,14.58842467,-11.875001,43.872219,174
Comoros,COM,1999,190.057812,14.68012073,-11.875001,43.872219,174
Comoros,COM,2000,186.7276742,14.99087691,-11.875001,43.872219,174
Comoros,COM,2001,179.7598444,15.12114127,-11.875001,43.872219,174
Comoros,COM,2002,172.9251736,15.30751796,-11.875001,43.872219,174
Comoros,COM,2003,164.7158168,15.35184627,-11.875001,43.872219,174
Comoros,COM,2004,156.625969,15.34848602,-11.875001,43.872219,174
Comoros,COM,2005,153.830961,15.80677135,-11.875001,43.872219,174
Comoros,COM,2006,147.4879733,15.80881403,-11.875001,43.872219,174
Comoros,COM,2007,148.7020969,16.46590742,-11.875001,43.872219,174
Comoros,COM,2008,147.2158799,16.72708324,-11.875001,43.872219,174
Comoros,COM,2009,141.3036115,16.48990896,-11.875001,43.872219,174
Comoros,COM,2010,136.8648395,16.54639201,-11.875001,43.872219,174
Comoros,COM,2011,135.5217223,17.22737687,-11.875001,43.872219,174
Comoros,COM,2012,133.0105461,17.91598281,-11.875001,43.872219,174
Comoros,COM,2013,129.9341155,18.57477525,-11.875001,43.872219,174
Comoros,COM,2014,131.1077448,19.55486295,-11.875001,43.872219,174
Comoros,COM,2015,127.9920068,19.58053921,-11.875001,43.872219,174
Comoros,COM,2016,124.6250128,19.02240145,-11.875001,43.872219,174
Comoros,COM,2017,121.5388974,18.60833769,-11.875001,43.872219,174
Comoros,COM,2018,117.0880482,18.98174038,-11.875001,43.872219,174
Comoros,COM,2019,113.3618183,19.82803998,-11.875001,43.872219,174
Republic of the Congo,COG,1990,224.4933883,44.30310525,-0.228021,15.827659,178
Republic of the Congo,COG,1991,216.8233547,44.89361136,-0.228021,15.827659,178
Republic of the Congo,COG,1992,210.2644055,45.48241718,-0.228021,15.827659,178
Republic of the Congo,COG,1993,206.250691,46.82224986,-0.228021,15.827659,178
Republic of the Congo,COG,1994,206.0754862,48.69857643,-0.228021,15.827659,178
Republic of the Congo,COG,1995,203.8365297,50.34289526,-0.228021,15.827659,178
Republic of the Congo,COG,1996,202.0643068,52.00528612,-0.228021,15.827659,178
Republic of the Congo,COG,1997,198.1233065,53.60096384,-0.228021,15.827659,178
Republic of the Congo,COG,1998,189.4920417,53.79064242,-0.228021,15.827659,178
Republic of the Congo,COG,1999,182.9172045,54.32641618,-0.228021,15.827659,178
Republic of the Congo,COG,2000,174.4900087,53.38986624,-0.228021,15.827659,178
Republic of the Congo,COG,2001,165.1136521,52.1254365,-0.228021,15.827659,178
Republic of the Congo,COG,2002,157.7194145,50.88772049,-0.228021,15.827659,178
Republic of the Congo,COG,2003,154.5442492,51.23975348,-0.228021,15.827659,178
Republic of the Congo,COG,2004,150.4082547,51.72672829,-0.228021,15.827659,178
Republic of the Congo,COG,2005,145.3092025,52.76566588,-0.228021,15.827659,178
Republic of the Congo,COG,2006,139.8349297,54.36266616,-0.228021,15.827659,178
Republic of the Congo,COG,2007,134.0942865,55.46705563,-0.228021,15.827659,178
Republic of the Congo,COG,2008,128.2961259,56.90262634,-0.228021,15.827659,178
Republic of the Congo,COG,2009,121.2674934,58.28469888,-0.228021,15.827659,178
Republic of the Congo,COG,2010,114.5699467,60.3229164,-0.228021,15.827659,178
Republic of the Congo,COG,2011,107.7887588,62.87756421,-0.228021,15.827659,178
Republic of the Congo,COG,2012,101.4919291,66.71929526,-0.228021,15.827659,178
Republic of the Congo,COG,2013,95.07527829,70.33119436,-0.228021,15.827659,178
Republic of the Congo,COG,2014,89.18228127,73.16081032,-0.228021,15.827659,178
Republic of the Congo,COG,2015,83.70530811,73.81366901,-0.228021,15.827659,178
Republic of the Congo,COG,2016,79.07162742,72.8629009,-0.228021,15.827659,178
Republic of the Congo,COG,2017,75.14130927,72.33739731,-0.228021,15.827659,178
Republic of the Congo,COG,2018,71.10083726,74.13260638,-0.228021,15.827659,178
Republic of the Congo,COG,2019,66.66997022,76.71752143,-0.228021,15.827659,178
Cook Islands,COK,1990,21.01297823,19.61967843,-21.236736,-159.777671,184
Cook Islands,COK,1991,19.03650725,19.28748772,-21.236736,-159.777671,184
Cook Islands,COK,1992,17.21694851,19.09572479,-21.236736,-159.777671,184
Cook Islands,COK,1993,15.56958101,18.85448538,-21.236736,-159.777671,184
Cook Islands,COK,1994,14.15177517,18.20008295,-21.236736,-159.777671,184
Cook Islands,COK,1995,12.9415056,17.56951389,-21.236736,-159.777671,184
Cook Islands,COK,1996,11.88211196,17.23985156,-21.236736,-159.777671,184
Cook Islands,COK,1997,10.95435218,17.27419849,-21.236736,-159.777671,184
Cook Islands,COK,1998,10.12271529,17.28674869,-21.236736,-159.777671,184
Cook Islands,COK,1999,9.35182867,17.12340295,-21.236736,-159.777671,184
Cook Islands,COK,2000,8.584287355,16.6654068,-21.236736,-159.777671,184
Cook Islands,COK,2001,7.725887909,16.17414434,-21.236736,-159.777671,184
Cook Islands,COK,2002,6.934229134,15.96647112,-21.236736,-159.777671,184
Cook Islands,COK,2003,6.216830724,15.66150931,-21.236736,-159.777671,184
Cook Islands,COK,2004,5.616887147,15.3594347,-21.236736,-159.777671,184
Cook Islands,COK,2005,5.167275006,14.98248004,-21.236736,-159.777671,184
Cook Islands,COK,2006,4.795853506,14.5131237,-21.236736,-159.777671,184
Cook Islands,COK,2007,4.508222177,13.88185756,-21.236736,-159.777671,184
Cook Islands,COK,2008,4.25273103,13.24576171,-21.236736,-159.777671,184
Cook Islands,COK,2009,4.073749444,12.71552674,-21.236736,-159.777671,184
Cook Islands,COK,2010,3.985897644,12.55436861,-21.236736,-159.777671,184
Cook Islands,COK,2011,3.940621799,12.52390262,-21.236736,-159.777671,184
Cook Islands,COK,2012,3.888236917,12.46497199,-21.236736,-159.777671,184
Cook Islands,COK,2013,3.826485248,12.54124094,-21.236736,-159.777671,184
Cook Islands,COK,2014,3.765649888,12.52826926,-21.236736,-159.777671,184
Cook Islands,COK,2015,3.711306512,12.65746014,-21.236736,-159.777671,184
Cook Islands,COK,2016,3.606010889,13.11400107,-21.236736,-159.777671,184
Cook Islands,COK,2017,3.444761731,13.39529258,-21.236736,-159.777671,184
Cook Islands,COK,2018,3.236114296,13.48519274,-21.236736,-159.777671,184
Cook Islands,COK,2019,2.960682217,13.30172852,-21.236736,-159.777671,184
Costa Rica,CRI,1990,26.45042579,21.46719908,9.748917,-83.753428,188
Costa Rica,CRI,1991,24.3091,21.52268598,9.748917,-83.753428,188
Costa Rica,CRI,1992,22.2024216,21.77884715,9.748917,-83.753428,188
Costa Rica,CRI,1993,19.92718079,21.62248163,9.748917,-83.753428,188
Costa Rica,CRI,1994,18.76868778,22.6874554,9.748917,-83.753428,188
Costa Rica,CRI,1995,17.458325,23.58495697,9.748917,-83.753428,188
Costa Rica,CRI,1996,14.98903456,22.97530241,9.748917,-83.753428,188
Costa Rica,CRI,1997,13.36054788,23.7214483,9.748917,-83.753428,188
Costa Rica,CRI,1998,11.89942083,24.45671857,9.748917,-83.753428,188
Costa Rica,CRI,1999,10.71079226,25.56647547,9.748917,-83.753428,188
Costa Rica,CRI,2000,9.279145271,24.77228586,9.748917,-83.753428,188
Costa Rica,CRI,2001,8.489814833,25.1473672,9.748917,-83.753428,188
Costa Rica,CRI,2002,7.311819051,23.64646935,9.748917,-83.753428,188
Costa Rica,CRI,2003,6.722677466,23.70911473,9.748917,-83.753428,188
Costa Rica,CRI,2004,6.146462419,23.14644023,9.748917,-83.753428,188
Costa Rica,CRI,2005,5.206491005,20.92001611,9.748917,-83.753428,188
Costa Rica,CRI,2006,4.920160592,21.31403337,9.748917,-83.753428,188
Costa Rica,CRI,2007,4.061924806,18.79553326,9.748917,-83.753428,188
Costa Rica,CRI,2008,3.819263789,18.8260128,9.748917,-83.753428,188
Costa Rica,CRI,2009,3.473451254,18.06350305,9.748917,-83.753428,188
Costa Rica,CRI,2010,3.613068685,20.18238902,9.748917,-83.753428,188
Costa Rica,CRI,2011,3.221998486,19.23667947,9.748917,-83.753428,188
Costa Rica,CRI,2012,2.998259349,19.29278152,9.748917,-83.753428,188
Costa Rica,CRI,2013,2.825952728,19.31017193,9.748917,-83.753428,188
Costa Rica,CRI,2014,2.647654401,19.2550764,9.748917,-83.753428,188
Costa Rica,CRI,2015,2.540988722,19.53818754,9.748917,-83.753428,188
Costa Rica,CRI,2016,2.496145164,19.75993642,9.748917,-83.753428,188
Costa Rica,CRI,2017,2.350593498,18.97554294,9.748917,-83.753428,188
Costa Rica,CRI,2018,2.206289835,19.18414998,9.748917,-83.753428,188
Costa Rica,CRI,2019,2.049038368,19.03814098,9.748917,-83.753428,188
Ivory Coast,CIV,1990,220.4447658,35.25086871,7.539989,-5.54708,384
Ivory Coast,CIV,1991,218.8088873,35.3375792,7.539989,-5.54708,384
Ivory Coast,CIV,1992,218.7048391,35.73180315,7.539989,-5.54708,384
Ivory Coast,CIV,1993,219.2707306,36.44560094,7.539989,-5.54708,384
Ivory Coast,CIV,1994,219.5232445,37.14224984,7.539989,-5.54708,384
Ivory Coast,CIV,1995,219.5092746,37.87857298,7.539989,-5.54708,384
Ivory Coast,CIV,1996,216.2380206,39.20866719,7.539989,-5.54708,384
Ivory Coast,CIV,1997,211.1275394,41.55819399,7.539989,-5.54708,384
Ivory Coast,CIV,1998,206.8029512,44.45943739,7.539989,-5.54708,384
Ivory Coast,CIV,1999,202.3694329,46.67770871,7.539989,-5.54708,384
Ivory Coast,CIV,2000,200.7562684,47.94660578,7.539989,-5.54708,384
Ivory Coast,CIV,2001,196.8638546,47.75321593,7.539989,-5.54708,384
Ivory Coast,CIV,2002,195.1071731,47.84624079,7.539989,-5.54708,384
Ivory Coast,CIV,2003,191.4477832,47.47835493,7.539989,-5.54708,384
Ivory Coast,CIV,2004,189.0118719,47.38878306,7.539989,-5.54708,384
Ivory Coast,CIV,2005,185.5724307,47.08158725,7.539989,-5.54708,384
Ivory Coast,CIV,2006,183.6231166,47.20938338,7.539989,-5.54708,384
Ivory Coast,CIV,2007,178.5588852,45.94774079,7.539989,-5.54708,384
Ivory Coast,CIV,2008,175.3956579,44.94518781,7.539989,-5.54708,384
Ivory Coast,CIV,2009,172.2936205,44.11443527,7.539989,-5.54708,384
Ivory Coast,CIV,2010,169.055057,43.85576911,7.539989,-5.54708,384
Ivory Coast,CIV,2011,164.439444,45.32740368,7.539989,-5.54708,384
Ivory Coast,CIV,2012,158.6601365,49.07289752,7.539989,-5.54708,384
Ivory Coast,CIV,2013,153.4989108,53.7935582,7.539989,-5.54708,384
Ivory Coast,CIV,2014,145.8374302,56.46511437,7.539989,-5.54708,384
Ivory Coast,CIV,2015,141.2669405,57.41012819,7.539989,-5.54708,384
Ivory Coast,CIV,2016,134.0616168,53.61359441,7.539989,-5.54708,384
Ivory Coast,CIV,2017,129.2150039,51.00140125,7.539989,-5.54708,384
Ivory Coast,CIV,2018,125.3086733,52.09628179,7.539989,-5.54708,384
Ivory Coast,CIV,2019,118.3630498,53.38041073,7.539989,-5.54708,384
Croatia,HRV,1990,15.815291,79.13137328,45.1,15.2,191
Croatia,HRV,1991,14.63327148,76.65694577,45.1,15.2,191
Croatia,HRV,1992,13.67736597,75.19629723,45.1,15.2,191
Croatia,HRV,1993,12.83761884,74.37460747,45.1,15.2,191
Croatia,HRV,1994,11.96512075,72.832248,45.1,15.2,191
Croatia,HRV,1995,11.25493527,72.1620678,45.1,15.2,191
Croatia,HRV,1996,10.71021602,72.10322124,45.1,15.2,191
Croatia,HRV,1997,10.15964216,72.15274109,45.1,15.2,191
Croatia,HRV,1998,9.326674701,69.72036751,45.1,15.2,191
Croatia,HRV,1999,8.528511513,67.47556329,45.1,15.2,191
Croatia,HRV,2000,7.613113908,63.61606885,45.1,15.2,191
Croatia,HRV,2001,6.947435991,61.69358578,45.1,15.2,191
Croatia,HRV,2002,6.504033781,61.63010256,45.1,15.2,191
Croatia,HRV,2003,6.139290794,62.02822045,45.1,15.2,191
Croatia,HRV,2004,5.499012161,58.97298975,45.1,15.2,191
Croatia,HRV,2005,5.158247408,58.5274315,45.1,15.2,191
Croatia,HRV,2006,4.710151608,56.06922118,45.1,15.2,191
Croatia,HRV,2007,4.467765398,55.48702983,45.1,15.2,191
Croatia,HRV,2008,4.173215669,54.05415826,45.1,15.2,191
Croatia,HRV,2009,3.744415904,50.44848346,45.1,15.2,191
Croatia,HRV,2010,3.461021462,48.2571674,45.1,15.2,191
Croatia,HRV,2011,3.177920176,46.34028328,45.1,15.2,191
Croatia,HRV,2012,2.928872848,44.75624912,45.1,15.2,191
Croatia,HRV,2013,2.658798712,42.05075246,45.1,15.2,191
Croatia,HRV,2014,2.515425339,41.22249988,45.1,15.2,191
Croatia,HRV,2015,2.467474493,41.54048864,45.1,15.2,191
Croatia,HRV,2016,2.181714707,37.09372387,45.1,15.2,191
Croatia,HRV,2017,2.074229484,35.60345766,45.1,15.2,191
Croatia,HRV,2018,1.947546726,35.25977859,45.1,15.2,191
Croatia,HRV,2019,1.834918416,35.34039757,45.1,15.2,191
Cuba,CUB,1990,7.522951023,46.69964232,21.521757,-77.781167,192
Cuba,CUB,1991,6.962668983,45.6362205,21.521757,-77.781167,192
Cuba,CUB,1992,6.663027674,46.07722454,21.521757,-77.781167,192
Cuba,CUB,1993,6.364155921,46.41679741,21.521757,-77.781167,192
Cuba,CUB,1994,5.978515667,45.87181812,21.521757,-77.781167,192
Cuba,CUB,1995,5.616421366,44.95094833,21.521757,-77.781167,192
Cuba,CUB,1996,5.294632383,44.45923189,21.521757,-77.781167,192
Cuba,CUB,1997,4.950054143,43.99748042,21.521757,-77.781167,192
Cuba,CUB,1998,4.71320675,44.26939815,21.521757,-77.781167,192
Cuba,CUB,1999,4.458283365,44.22182787,21.521757,-77.781167,192
Cuba,CUB,2000,4.124290923,42.61285427,21.521757,-77.781167,192
Cuba,CUB,2001,3.887450015,41.79398876,21.521757,-77.781167,192
Cuba,CUB,2002,3.414808936,38.3520745,21.521757,-77.781167,192
Cuba,CUB,2003,3.236530273,37.99240382,21.521757,-77.781167,192
Cuba,CUB,2004,3.054951651,37.50197703,21.521757,-77.781167,192
Cuba,CUB,2005,2.914792448,37.26628419,21.521757,-77.781167,192
Cuba,CUB,2006,2.607717304,34.48323526,21.521757,-77.781167,192
Cuba,CUB,2007,2.480605571,33.63671279,21.521757,-77.781167,192
Cuba,CUB,2008,2.399795116,33.25635556,21.521757,-77.781167,192
Cuba,CUB,2009,2.282586156,32.72955917,21.521757,-77.781167,192
Cuba,CUB,2010,2.167139027,32.54309368,21.521757,-77.781167,192
Cuba,CUB,2011,1.913558875,30.74395235,21.521757,-77.781167,192
Cuba,CUB,2012,1.801868888,31.88894875,21.521757,-77.781167,192
Cuba,CUB,2013,1.669469588,32.88832312,21.521757,-77.781167,192
Cuba,CUB,2014,1.54697323,33.7768071,21.521757,-77.781167,192
Cuba,CUB,2015,1.458254756,34.98857095,21.521757,-77.781167,192
Cuba,CUB,2016,1.316909909,33.42538813,21.521757,-77.781167,192
Cuba,CUB,2017,1.241724298,32.9151765,21.521757,-77.781167,192
Cuba,CUB,2018,1.147222482,32.24746826,21.521757,-77.781167,192
Cuba,CUB,2019,1.028777035,30.6053334,21.521757,-77.781167,192
Cyprus,CYP,1990,1.478247521,61.750797,35.126413,33.429859,196
Cyprus,CYP,1991,1.336687215,65.40845546,35.126413,33.429859,196
Cyprus,CYP,1992,1.202377571,68.31112936,35.126413,33.429859,196
Cyprus,CYP,1993,1.055958343,69.15108074,35.126413,33.429859,196
Cyprus,CYP,1994,0.900804234,67.24270486,35.126413,33.429859,196
Cyprus,CYP,1995,0.771754074,65.15912352,35.126413,33.429859,196
Cyprus,CYP,1996,0.658639419,62.14377261,35.126413,33.429859,196
Cyprus,CYP,1997,0.570978987,59.90630817,35.126413,33.429859,196
Cyprus,CYP,1998,0.504411804,58.14894637,35.126413,33.429859,196
Cyprus,CYP,1999,0.441331725,56.14926924,35.126413,33.429859,196
Cyprus,CYP,2000,0.373220387,53.25963298,35.126413,33.429859,196
Cyprus,CYP,2001,0.316717006,50.67921153,35.126413,33.429859,196
Cyprus,CYP,2002,0.271929591,48.73812152,35.126413,33.429859,196
Cyprus,CYP,2003,0.234137868,46.71122279,35.126413,33.429859,196
Cyprus,CYP,2004,0.203349449,45.43258841,35.126413,33.429859,196
Cyprus,CYP,2005,0.179274919,44.35268397,35.126413,33.429859,196
Cyprus,CYP,2006,0.158587133,43.89179139,35.126413,33.429859,196
Cyprus,CYP,2007,0.138026455,42.84578448,35.126413,33.429859,196
Cyprus,CYP,2008,0.117895471,41.43529524,35.126413,33.429859,196
Cyprus,CYP,2009,0.101237395,39.64694121,35.126413,33.429859,196
Cyprus,CYP,2010,0.090285886,38.6510157,35.126413,33.429859,196
Cyprus,CYP,2011,0.082048923,36.8345196,35.126413,33.429859,196
Cyprus,CYP,2012,0.075297921,35.36762651,35.126413,33.429859,196
Cyprus,CYP,2013,0.069920747,33.89970806,35.126413,33.429859,196
Cyprus,CYP,2014,0.06597517,32.67355162,35.126413,33.429859,196
Cyprus,CYP,2015,0.062018871,31.46348325,35.126413,33.429859,196
Cyprus,CYP,2016,0.057115089,28.35970143,35.126413,33.429859,196
Cyprus,CYP,2017,0.052988338,26.06197254,35.126413,33.429859,196
Cyprus,CYP,2018,0.049394201,25.87694962,35.126413,33.429859,196
Cyprus,CYP,2019,0.046445878,26.34678785,35.126413,33.429859,196
Czechia,CZE,1990,3.429601528,98.0773613,49.817492,15.472962,203
Czechia,CZE,1991,2.989105056,92.80164798,49.817492,15.472962,203
Czechia,CZE,1992,2.636994399,89.27897623,49.817492,15.472962,203
Czechia,CZE,1993,2.313782403,84.72274555,49.817492,15.472962,203
Czechia,CZE,1994,2.072899872,81.87630995,49.817492,15.472962,203
Czechia,CZE,1995,1.915181433,80.20096306,49.817492,15.472962,203
Czechia,CZE,1996,1.696400709,74.50340391,49.817492,15.472962,203
Czechia,CZE,1997,1.582257467,71.39817012,49.817492,15.472962,203
Czechia,CZE,1998,1.422284763,65.55763178,49.817492,15.472962,203
Czechia,CZE,1999,1.315423818,62.02451611,49.817492,15.472962,203
Czechia,CZE,2000,1.227490752,59.58063659,49.817492,15.472962,203
Czechia,CZE,2001,1.148173915,57.84084762,49.817492,15.472962,203
Czechia,CZE,2002,1.06390135,55.95954179,49.817492,15.472962,203
Czechia,CZE,2003,1.02540651,56.0777358,49.817492,15.472962,203
Czechia,CZE,2004,0.926631038,52.74296551,49.817492,15.472962,203
Czechia,CZE,2005,0.866462232,50.89670085,49.817492,15.472962,203
Czechia,CZE,2006,0.786869213,47.91884409,49.817492,15.472962,203
Czechia,CZE,2007,0.735124734,46.46967035,49.817492,15.472962,203
Czechia,CZE,2008,0.695566189,45.41236429,49.817492,15.472962,203
Czechia,CZE,2009,0.650447677,43.88327349,49.817492,15.472962,203
Czechia,CZE,2010,0.609660117,42.39447351,49.817492,15.472962,203
Czechia,CZE,2011,0.579241246,41.03496857,49.817492,15.472962,203
Czechia,CZE,2012,0.548379104,39.11019355,49.817492,15.472962,203
Czechia,CZE,2013,0.520316606,37.10705673,49.817492,15.472962,203
Czechia,CZE,2014,0.483906265,34.5251264,49.817492,15.472962,203
Czechia,CZE,2015,0.465844839,33.37838909,49.817492,15.472962,203
Czechia,CZE,2016,0.437530105,31.58376588,49.817492,15.472962,203
Czechia,CZE,2017,0.41258558,30.53881406,49.817492,15.472962,203
Czechia,CZE,2018,0.39556458,30.73540955,49.817492,15.472962,203
Czechia,CZE,2019,0.369566789,30.19125941,49.817492,15.472962,203
Democratic Republic of the Congo,COD,1990,249.6598734,28.03484809,-4.038333,21.758664,203
Democratic Republic of the Congo,COD,1991,248.1220956,28.46373119,-4.038333,21.758664,203
Democratic Republic of the Congo,COD,1992,245.8453776,28.22110788,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1993,242.8372375,27.93788189,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1994,242.0868691,27.56111099,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1995,242.2529441,27.69545532,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1996,245.2063919,27.71870769,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1997,240.2625476,26.92093427,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1998,239.9660303,26.19815247,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,1999,238.9360657,25.6085957,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2000,239.2218387,24.44170891,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2001,238.9024304,23.73913184,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2002,236.8300832,22.26537548,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2003,238.9460488,21.77100402,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2004,236.7103772,21.5850843,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2005,233.3924306,22.38788128,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2006,231.0029509,23.4498031,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2007,227.5284574,23.01407275,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2008,225.2856896,22.39322726,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2009,221.0861618,22.16823327,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2010,216.5459094,22.82108518,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2011,211.2350091,24.49014067,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2012,204.0132706,27.18973185,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2013,194.4729935,29.80361175,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2014,185.090312,31.65604495,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2015,176.8826362,31.8339889,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2016,170.2723187,31.31157527,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2017,165.1486241,31.09503176,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2018,161.6172534,32.76060384,-4.038333,21.758664,180
Democratic Republic of the Congo,COD,2019,156.9232073,34.45507317,-4.038333,21.758664,180
Denmark,DNK,1990,0.167865778,45.41077748,56.26392,9.501785,208
Denmark,DNK,1991,0.154858031,43.49126015,56.26392,9.501785,208
Denmark,DNK,1992,0.145070796,42.18355389,56.26392,9.501785,208
Denmark,DNK,1993,0.13569817,41.30213466,56.26392,9.501785,208
Denmark,DNK,1994,0.125147829,39.8527036,56.26392,9.501785,208
Denmark,DNK,1995,0.115412966,38.74071881,56.26392,9.501785,208
Denmark,DNK,1996,0.104184305,36.89415329,56.26392,9.501785,208
Denmark,DNK,1997,0.093573634,34.89449284,56.26392,9.501785,208
Denmark,DNK,1998,0.0836257,33.09676325,56.26392,9.501785,208
Denmark,DNK,1999,0.07785486,32.21754757,56.26392,9.501785,208
Denmark,DNK,2000,0.069886558,30.17548049,56.26392,9.501785,208
Denmark,DNK,2001,0.065378345,29.14745908,56.26392,9.501785,208
Denmark,DNK,2002,0.060840024,28.27295473,56.26392,9.501785,208
Denmark,DNK,2003,0.055477094,26.7339909,56.26392,9.501785,208
Denmark,DNK,2004,0.050269503,24.92797437,56.26392,9.501785,208
Denmark,DNK,2005,0.045627606,23.54227537,56.26392,9.501785,208
Denmark,DNK,2006,0.042428678,22.97455728,56.26392,9.501785,208
Denmark,DNK,2007,0.039563233,22.7427145,56.26392,9.501785,208
Denmark,DNK,2008,0.036478927,21.95703291,56.26392,9.501785,208
Denmark,DNK,2009,0.034081954,21.65307718,56.26392,9.501785,208
Denmark,DNK,2010,0.031434651,20.89632069,56.26392,9.501785,208
Denmark,DNK,2011,0.028610058,19.40538814,56.26392,9.501785,208
Denmark,DNK,2012,0.026304162,17.69616831,56.26392,9.501785,208
Denmark,DNK,2013,0.024306001,15.84455821,56.26392,9.501785,208
Denmark,DNK,2014,0.022360002,14.10168349,56.26392,9.501785,208
Denmark,DNK,2015,0.020880964,13.12646321,56.26392,9.501785,208
Denmark,DNK,2016,0.019954274,12.93848861,56.26392,9.501785,208
Denmark,DNK,2017,0.019034968,12.82782433,56.26392,9.501785,208
Denmark,DNK,2018,0.017945437,12.75029848,56.26392,9.501785,208
Denmark,DNK,2019,0.016715848,12.07821355,56.26392,9.501785,208
Djibouti,DJI,1990,142.9479654,29.97085711,11.825138,42.590275,262
Djibouti,DJI,1991,143.012477,30.8538787,11.825138,42.590275,262
Djibouti,DJI,1992,140.5222886,31.76193569,11.825138,42.590275,262
Djibouti,DJI,1993,137.1311533,32.94649968,11.825138,42.590275,262
Djibouti,DJI,1994,131.9642841,33.91673019,11.825138,42.590275,262
Djibouti,DJI,1995,129.4696374,35.80182384,11.825138,42.590275,262
Djibouti,DJI,1996,124.1138739,37.3752619,11.825138,42.590275,262
Djibouti,DJI,1997,117.7862342,39.55402378,11.825138,42.590275,262
Djibouti,DJI,1998,112.7902839,42.75448331,11.825138,42.590275,262
Djibouti,DJI,1999,106.3209695,45.86648563,11.825138,42.590275,262
Djibouti,DJI,2000,99.19857057,48.36079427,11.825138,42.590275,262
Djibouti,DJI,2001,90.68391696,51.11844975,11.825138,42.590275,262
Djibouti,DJI,2002,81.17852067,54.63312511,11.825138,42.590275,262
Djibouti,DJI,2003,71.42301187,58.09431398,11.825138,42.590275,262
Djibouti,DJI,2004,64.97393966,62.8450514,11.825138,42.590275,262
Djibouti,DJI,2005,59.92690138,65.40584327,11.825138,42.590275,262
Djibouti,DJI,2006,57.07037957,67.04776123,11.825138,42.590275,262
Djibouti,DJI,2007,54.95651575,68.42876857,11.825138,42.590275,262
Djibouti,DJI,2008,53.06855599,69.17171566,11.825138,42.590275,262
Djibouti,DJI,2009,51.09035639,69.5463653,11.825138,42.590275,262
Djibouti,DJI,2010,49.68368624,71.03624616,11.825138,42.590275,262
Djibouti,DJI,2011,47.93433969,72.36386045,11.825138,42.590275,262
Djibouti,DJI,2012,46.32483406,73.6697164,11.825138,42.590275,262
Djibouti,DJI,2013,44.76103568,74.899427,11.825138,42.590275,262
Djibouti,DJI,2014,42.60489809,74.81211515,11.825138,42.590275,262
Djibouti,DJI,2015,41.00177703,75.59265626,11.825138,42.590275,262
Djibouti,DJI,2016,38.88371662,75.28078249,11.825138,42.590275,262
Djibouti,DJI,2017,36.94618242,75.67419625,11.825138,42.590275,262
Djibouti,DJI,2018,34.97549463,76.69513062,11.825138,42.590275,262
Djibouti,DJI,2019,32.75424414,77.56065923,11.825138,42.590275,262
Dominica,DMA,1990,49.30958246,33.09365385,15.414999,-61.370976,212
Dominica,DMA,1991,44.93285099,34.16468085,15.414999,-61.370976,212
Dominica,DMA,1992,39.34674566,34.18235191,15.414999,-61.370976,212
Dominica,DMA,1993,35.15198477,34.72267368,15.414999,-61.370976,212
Dominica,DMA,1994,31.69489069,35.44669979,15.414999,-61.370976,212
Dominica,DMA,1995,28.48128278,35.97046355,15.414999,-61.370976,212
Dominica,DMA,1996,25.57327577,36.49064744,15.414999,-61.370976,212
Dominica,DMA,1997,22.58877702,36.66278332,15.414999,-61.370976,212
Dominica,DMA,1998,19.98027722,36.78163958,15.414999,-61.370976,212
Dominica,DMA,1999,18.21898064,37.68999577,15.414999,-61.370976,212
Dominica,DMA,2000,16.38387641,37.51063801,15.414999,-61.370976,212
Dominica,DMA,2001,14.73014408,36.97487635,15.414999,-61.370976,212
Dominica,DMA,2002,13.4387844,36.7009664,15.414999,-61.370976,212
Dominica,DMA,2003,12.26175104,36.34942924,15.414999,-61.370976,212
Dominica,DMA,2004,11.0097922,35.20532795,15.414999,-61.370976,212
Dominica,DMA,2005,10.05364033,34.41189781,15.414999,-61.370976,212
Dominica,DMA,2006,9.447072402,34.43093861,15.414999,-61.370976,212
Dominica,DMA,2007,8.928202583,34.56449059,15.414999,-61.370976,212
Dominica,DMA,2008,8.390235484,34.43178098,15.414999,-61.370976,212
Dominica,DMA,2009,7.934607784,34.49890794,15.414999,-61.370976,212
Dominica,DMA,2010,7.534816183,34.75560125,15.414999,-61.370976,212
Dominica,DMA,2011,7.153699651,35.46227268,15.414999,-61.370976,212
Dominica,DMA,2012,6.775883116,36.61396244,15.414999,-61.370976,212
Dominica,DMA,2013,6.387395165,37.61730418,15.414999,-61.370976,212
Dominica,DMA,2014,6.015474194,38.33953356,15.414999,-61.370976,212
Dominica,DMA,2015,5.689124558,38.54162006,15.414999,-61.370976,212
Dominica,DMA,2016,5.394236369,37.23306234,15.414999,-61.370976,212
Dominica,DMA,2017,5.175152324,36.15889301,15.414999,-61.370976,212
Dominica,DMA,2018,5.00317648,36.43692136,15.414999,-61.370976,212
Dominica,DMA,2019,4.834427685,37.15631227,15.414999,-61.370976,212
Dominican Republic,DOM,1990,62.2658921,16.53953198,18.735693,-70.162651,214
Dominican Republic,DOM,1991,56.73058676,15.9608533,18.735693,-70.162651,214
Dominican Republic,DOM,1992,51.63276197,15.5667919,18.735693,-70.162651,214
Dominican Republic,DOM,1993,48.41394544,15.67064365,18.735693,-70.162651,214
Dominican Republic,DOM,1994,44.24187187,15.65667663,18.735693,-70.162651,214
Dominican Republic,DOM,1995,41.47948379,16.12401689,18.735693,-70.162651,214
Dominican Republic,DOM,1996,39.88170062,17.19594884,18.735693,-70.162651,214
Dominican Republic,DOM,1997,38.45185251,18.54198332,18.735693,-70.162651,214
Dominican Republic,DOM,1998,36.41327862,19.76976817,18.735693,-70.162651,214
Dominican Republic,DOM,1999,34.18631374,21.06350581,18.735693,-70.162651,214
Dominican Republic,DOM,2000,31.44911775,21.56215576,18.735693,-70.162651,214
Dominican Republic,DOM,2001,29.06869114,22.50762916,18.735693,-70.162651,214
Dominican Republic,DOM,2002,26.80765805,23.65711664,18.735693,-70.162651,214
Dominican Republic,DOM,2003,25.80169054,25.94471927,18.735693,-70.162651,214
Dominican Republic,DOM,2004,25.2800595,28.44331112,18.735693,-70.162651,214
Dominican Republic,DOM,2005,24.05406667,30.09681387,18.735693,-70.162651,214
Dominican Republic,DOM,2006,22.48502692,31.22913026,18.735693,-70.162651,214
Dominican Republic,DOM,2007,20.78065451,31.94681447,18.735693,-70.162651,214
Dominican Republic,DOM,2008,19.11147366,32.39118806,18.735693,-70.162651,214
Dominican Republic,DOM,2009,17.80078193,33.0075963,18.735693,-70.162651,214
Dominican Republic,DOM,2010,16.68620104,33.64581151,18.735693,-70.162651,214
Dominican Republic,DOM,2011,15.83276643,34.7446936,18.735693,-70.162651,214
Dominican Republic,DOM,2012,15.71711973,37.51691834,18.735693,-70.162651,214
Dominican Republic,DOM,2013,15.8008446,40.77465298,18.735693,-70.162651,214
Dominican Republic,DOM,2014,15.47684458,42.89137141,18.735693,-70.162651,214
Dominican Republic,DOM,2015,14.95100545,44.48837777,18.735693,-70.162651,214
Dominican Republic,DOM,2016,13.78821845,44.22827965,18.735693,-70.162651,214
Dominican Republic,DOM,2017,12.4125235,42.96461293,18.735693,-70.162651,214
Dominican Republic,DOM,2018,11.25905435,42.3040389,18.735693,-70.162651,214
Dominican Republic,DOM,2019,10.26745669,41.90067741,18.735693,-70.162651,214
Ecuador,ECU,1990,33.42227243,31.09926356,-1.831239,-78.183406,218
Ecuador,ECU,1991,31.7891328,32.13260547,-1.831239,-78.183406,218
Ecuador,ECU,1992,28.30849637,30.8486716,-1.831239,-78.183406,218
Ecuador,ECU,1993,24.93122292,29.3903093,-1.831239,-78.183406,218
Ecuador,ECU,1994,22.25296039,28.30040905,-1.831239,-78.183406,218
Ecuador,ECU,1995,20.01520517,27.20466453,-1.831239,-78.183406,218
Ecuador,ECU,1996,19.01770999,27.47166208,-1.831239,-78.183406,218
Ecuador,ECU,1997,16.91293549,25.76277549,-1.831239,-78.183406,218
Ecuador,ECU,1998,16.13231252,25.99700454,-1.831239,-78.183406,218
Ecuador,ECU,1999,15.17043375,25.96513009,-1.831239,-78.183406,218
Ecuador,ECU,2000,14.09480523,25.65851384,-1.831239,-78.183406,218
Ecuador,ECU,2001,12.45388723,25.10650176,-1.831239,-78.183406,218
Ecuador,ECU,2002,12.479037,27.72118729,-1.831239,-78.183406,218
Ecuador,ECU,2003,11.67818373,29.11172085,-1.831239,-78.183406,218
Ecuador,ECU,2004,10.6816621,29.89243952,-1.831239,-78.183406,218
Ecuador,ECU,2005,10.17085802,31.57475012,-1.831239,-78.183406,218
Ecuador,ECU,2006,9.603369226,32.63392774,-1.831239,-78.183406,218
Ecuador,ECU,2007,8.993758037,33.33614411,-1.831239,-78.183406,218
Ecuador,ECU,2008,8.402418898,33.75454643,-1.831239,-78.183406,218
Ecuador,ECU,2009,7.72925365,33.41991376,-1.831239,-78.183406,218
Ecuador,ECU,2010,7.223333384,33.59876171,-1.831239,-78.183406,218
Ecuador,ECU,2011,6.514465187,32.88872662,-1.831239,-78.183406,218
Ecuador,ECU,2012,6.123137626,33.35773131,-1.831239,-78.183406,218
Ecuador,ECU,2013,5.646464925,33.23444481,-1.831239,-78.183406,218
Ecuador,ECU,2014,5.166617633,32.91833372,-1.831239,-78.183406,218
Ecuador,ECU,2015,4.690394765,32.30868874,-1.831239,-78.183406,218
Ecuador,ECU,2016,4.366299533,31.48181594,-1.831239,-78.183406,218
Ecuador,ECU,2017,4.081219674,30.50236324,-1.831239,-78.183406,218
Ecuador,ECU,2018,3.777747253,30.7726516,-1.831239,-78.183406,218
Ecuador,ECU,2019,3.444011613,31.02477169,-1.831239,-78.183406,218
Egypt,EGY,1990,27.66658579,174.3086558,26.820553,30.802498,818
Egypt,EGY,1991,23.34669161,176.0152551,26.820553,30.802498,818
Egypt,EGY,1992,19.32204895,175.5364153,26.820553,30.802498,818
Egypt,EGY,1993,16.39193161,180.6974908,26.820553,30.802498,818
Egypt,EGY,1994,13.74546931,183.6737325,26.820553,30.802498,818
Egypt,EGY,1995,11.25859407,179.6412519,26.820553,30.802498,818
Egypt,EGY,1996,9.401115311,176.5401701,26.820553,30.802498,818
Egypt,EGY,1997,7.934654969,176.879666,26.820553,30.802498,818
Egypt,EGY,1998,6.623848293,176.0697257,26.820553,30.802498,818
Egypt,EGY,1999,5.437357879,173.8586991,26.820553,30.802498,818
Egypt,EGY,2000,4.287756478,165.0677782,26.820553,30.802498,818
Egypt,EGY,2001,3.620414099,171.1739686,26.820553,30.802498,818
Egypt,EGY,2002,2.944866511,176.6021209,26.820553,30.802498,818
Egypt,EGY,2003,2.358235427,184.4467443,26.820553,30.802498,818
Egypt,EGY,2004,1.789723161,183.4744819,26.820553,30.802498,818
Egypt,EGY,2005,1.389091987,179.0225315,26.820553,30.802498,818
Egypt,EGY,2006,1.136322301,177.4789409,26.820553,30.802498,818
Egypt,EGY,2007,0.925023007,175.703691,26.820553,30.802498,818
Egypt,EGY,2008,0.774567117,178.1572627,26.820553,30.802498,818
Egypt,EGY,2009,0.655305084,180.4760831,26.820553,30.802498,818
Egypt,EGY,2010,0.555455672,179.8732312,26.820553,30.802498,818
Egypt,EGY,2011,0.467148379,176.7194188,26.820553,30.802498,818
Egypt,EGY,2012,0.409452853,178.1938774,26.820553,30.802498,818
Egypt,EGY,2013,0.34081676,170.8194245,26.820553,30.802498,818
Egypt,EGY,2014,0.295649025,169.970794,26.820553,30.802498,818
Egypt,EGY,2015,0.263274018,175.8940015,26.820553,30.802498,818
Egypt,EGY,2016,0.222082626,171.8709256,26.820553,30.802498,818
Egypt,EGY,2017,0.182671378,164.2782512,26.820553,30.802498,818
Egypt,EGY,2018,0.152629617,162.1564386,26.820553,30.802498,818
Egypt,EGY,2019,0.127176815,160.7194762,26.820553,30.802498,818
El Salvador,SLV,1990,79.42517744,22.63025712,13.794185,-88.89653,222
El Salvador,SLV,1991,76.24686786,22.21631862,13.794185,-88.89653,222
El Salvador,SLV,1992,75.49173082,22.78859068,13.794185,-88.89653,222
El Salvador,SLV,1993,73.98491679,23.25960784,13.794185,-88.89653,222
El Salvador,SLV,1994,71.71773926,23.84933871,13.794185,-88.89653,222
El Salvador,SLV,1995,65.97748976,23.47800798,13.794185,-88.89653,222
El Salvador,SLV,1996,61.65001084,23.61354462,13.794185,-88.89653,222
El Salvador,SLV,1997,58.27369129,25.12236286,13.794185,-88.89653,222
El Salvador,SLV,1998,56.49413012,28.18218598,13.794185,-88.89653,222
El Salvador,SLV,1999,49.16071073,27.56547227,13.794185,-88.89653,222
El Salvador,SLV,2000,45.20580114,27.53532173,13.794185,-88.89653,222
El Salvador,SLV,2001,42.03111833,27.23128773,13.794185,-88.89653,222
El Salvador,SLV,2002,37.98540148,25.83135695,13.794185,-88.89653,222
El Salvador,SLV,2003,36.7347889,26.55250845,13.794185,-88.89653,222
El Salvador,SLV,2004,35.92542002,26.77216025,13.794185,-88.89653,222
El Salvador,SLV,2005,34.36944429,26.61795976,13.794185,-88.89653,222
El Salvador,SLV,2006,32.93743099,26.88342686,13.794185,-88.89653,222
El Salvador,SLV,2007,31.21906524,26.50120502,13.794185,-88.89653,222
El Salvador,SLV,2008,29.1532761,25.89375695,13.794185,-88.89653,222
El Salvador,SLV,2009,29.27174348,27.23811257,13.794185,-88.89653,222
El Salvador,SLV,2010,26.18744703,25.99008358,13.794185,-88.89653,222
El Salvador,SLV,2011,24.96574607,27.47522283,13.794185,-88.89653,222
El Salvador,SLV,2012,21.56118369,27.27604926,13.794185,-88.89653,222
El Salvador,SLV,2013,20.30946289,29.84387166,13.794185,-88.89653,222
El Salvador,SLV,2014,19.15217157,33.05970058,13.794185,-88.89653,222
El Salvador,SLV,2015,16.87882497,33.27531279,13.794185,-88.89653,222
El Salvador,SLV,2016,14.52169461,32.29084763,13.794185,-88.89653,222
El Salvador,SLV,2017,12.60289524,31.51117759,13.794185,-88.89653,222
El Salvador,SLV,2018,11.0957477,31.48358606,13.794185,-88.89653,222
El Salvador,SLV,2019,9.972798683,31.74362111,13.794185,-88.89653,222
Equatorial Guinea,GNQ,1990,285.5198638,21.7727996,1.650801,10.267895,226
Equatorial Guinea,GNQ,1991,279.6698462,21.65823841,1.650801,10.267895,226
Equatorial Guinea,GNQ,1992,270.807328,21.66622014,1.650801,10.267895,226
Equatorial Guinea,GNQ,1993,263.4003369,22.11520221,1.650801,10.267895,226
Equatorial Guinea,GNQ,1994,255.2994509,22.70288539,1.650801,10.267895,226
Equatorial Guinea,GNQ,1995,247.9362107,23.62456183,1.650801,10.267895,226
Equatorial Guinea,GNQ,1996,238.3129155,25.56488439,1.650801,10.267895,226
Equatorial Guinea,GNQ,1997,215.7231219,27.91810573,1.650801,10.267895,226
Equatorial Guinea,GNQ,1998,197.1835625,31.36605173,1.650801,10.267895,226
Equatorial Guinea,GNQ,1999,180.163903,34.87628618,1.650801,10.267895,226
Equatorial Guinea,GNQ,2000,163.9547618,37.29681673,1.650801,10.267895,226
Equatorial Guinea,GNQ,2001,145.8113083,38.40893025,1.650801,10.267895,226
Equatorial Guinea,GNQ,2002,129.2554184,39.5083668,1.650801,10.267895,226
Equatorial Guinea,GNQ,2003,117.1814273,41.7890803,1.650801,10.267895,226
Equatorial Guinea,GNQ,2004,106.5355168,44.38769338,1.650801,10.267895,226
Equatorial Guinea,GNQ,2005,96.52921994,47.10429252,1.650801,10.267895,226
Equatorial Guinea,GNQ,2006,87.28301351,50.1979325,1.650801,10.267895,226
Equatorial Guinea,GNQ,2007,77.39927961,52.55728377,1.650801,10.267895,226
Equatorial Guinea,GNQ,2008,68.49386759,55.01456361,1.650801,10.267895,226
Equatorial Guinea,GNQ,2009,60.47900876,57.92933744,1.650801,10.267895,226
Equatorial Guinea,GNQ,2010,53.66671107,61.40545733,1.650801,10.267895,226
Equatorial Guinea,GNQ,2011,48.02603396,66.87682596,1.650801,10.267895,226
Equatorial Guinea,GNQ,2012,41.5775132,71.86534977,1.650801,10.267895,226
Equatorial Guinea,GNQ,2013,35.18830113,75.83501707,1.650801,10.267895,226
Equatorial Guinea,GNQ,2014,29.85573673,78.52872494,1.650801,10.267895,226
Equatorial Guinea,GNQ,2015,26.3943628,81.0522903,1.650801,10.267895,226
Equatorial Guinea,GNQ,2016,23.82736091,80.24328572,1.650801,10.267895,226
Equatorial Guinea,GNQ,2017,21.51841564,79.09220158,1.650801,10.267895,226
Equatorial Guinea,GNQ,2018,19.21455448,81.27897222,1.650801,10.267895,226
Equatorial Guinea,GNQ,2019,16.91805094,84.1575511,1.650801,10.267895,226
Eritrea,ERI,1990,253.2590326,25.96316217,15.179384,39.782334,232
Eritrea,ERI,1991,248.5996403,26.20040433,15.179384,39.782334,232
Eritrea,ERI,1992,240.0609322,26.29351456,15.179384,39.782334,232
Eritrea,ERI,1993,234.0755843,26.9083173,15.179384,39.782334,232
Eritrea,ERI,1994,231.8673088,28.08980346,15.179384,39.782334,232
Eritrea,ERI,1995,232.7269602,29.93375788,15.179384,39.782334,232
Eritrea,ERI,1996,225.847787,31.09785082,15.179384,39.782334,232
Eritrea,ERI,1997,219.0320674,33.16598128,15.179384,39.782334,232
Eritrea,ERI,1998,211.282811,35.17726075,15.179384,39.782334,232
Eritrea,ERI,1999,206.1720504,37.39179356,15.179384,39.782334,232
Eritrea,ERI,2000,201.3139325,38.18877346,15.179384,39.782334,232
Eritrea,ERI,2001,195.9484532,38.08311573,15.179384,39.782334,232
Eritrea,ERI,2002,194.6116685,38.53552734,15.179384,39.782334,232
Eritrea,ERI,2003,192.3154947,38.87971402,15.179384,39.782334,232
Eritrea,ERI,2004,191.6131554,39.43123378,15.179384,39.782334,232
Eritrea,ERI,2005,189.5052475,39.85239498,15.179384,39.782334,232
Eritrea,ERI,2006,187.1660105,40.44627886,15.179384,39.782334,232
Eritrea,ERI,2007,184.9286523,41.06050873,15.179384,39.782334,232
Eritrea,ERI,2008,183.1946847,41.38126852,15.179384,39.782334,232
Eritrea,ERI,2009,180.5693414,41.28915732,15.179384,39.782334,232
Eritrea,ERI,2010,178.1456235,41.58791277,15.179384,39.782334,232
Eritrea,ERI,2011,174.711504,42.02387167,15.179384,39.782334,232
Eritrea,ERI,2012,171.3695212,42.69298216,15.179384,39.782334,232
Eritrea,ERI,2013,167.929714,43.5405101,15.179384,39.782334,232
Eritrea,ERI,2014,163.8778426,44.45404485,15.179384,39.782334,232
Eritrea,ERI,2015,159.5550351,45.61379219,15.179384,39.782334,232
Eritrea,ERI,2016,154.7485194,47.05696009,15.179384,39.782334,232
Eritrea,ERI,2017,149.4776948,48.54212251,15.179384,39.782334,232
Eritrea,ERI,2018,144.6490074,49.92573602,15.179384,39.782334,232
Eritrea,ERI,2019,139.6690132,51.31304789,15.179384,39.782334,232
Estonia,EST,1990,23.15866593,35.97563602,58.595272,25.013607,233
Estonia,EST,1991,22.06738297,36.71569512,58.595272,25.013607,233
Estonia,EST,1992,20.03691758,35.76832238,58.595272,25.013607,233
Estonia,EST,1993,19.73482394,37.58255658,58.595272,25.013607,233
Estonia,EST,1994,19.41752121,39.25157013,58.595272,25.013607,233
Estonia,EST,1995,17.03413695,36.36462458,58.595272,25.013607,233
Estonia,EST,1996,14.13494558,31.32393345,58.595272,25.013607,233
Estonia,EST,1997,12.97889653,29.73470089,58.595272,25.013607,233
Estonia,EST,1998,12.57434458,29.62339508,58.595272,25.013607,233
Estonia,EST,1999,11.15282602,26.88567523,58.595272,25.013607,233
Estonia,EST,2000,10.32713297,25.72024774,58.595272,25.013607,233
Estonia,EST,2001,9.91048191,25.76738323,58.595272,25.013607,233
Estonia,EST,2002,8.991801757,24.31285485,58.595272,25.013607,233
Estonia,EST,2003,8.251825231,23.02594962,58.595272,25.013607,233
Estonia,EST,2004,7.493050818,21.77261735,58.595272,25.013607,233
Estonia,EST,2005,6.793943295,20.60321883,58.595272,25.013607,233
Estonia,EST,2006,6.159576885,19.79897638,58.595272,25.013607,233
Estonia,EST,2007,5.590829821,19.24771132,58.595272,25.013607,233
Estonia,EST,2008,4.721790196,17.28886507,58.595272,25.013607,233
Estonia,EST,2009,4.050864413,15.99648792,58.595272,25.013607,233
Estonia,EST,2010,3.380546195,14.31285738,58.595272,25.013607,233
Estonia,EST,2011,3.050244841,13.54827668,58.595272,25.013607,233
Estonia,EST,2012,2.679849092,12.04160599,58.595272,25.013607,233
Estonia,EST,2013,2.290870819,10.06738054,58.595272,25.013607,233
Estonia,EST,2014,2.035078152,8.743294505,58.595272,25.013607,233
Estonia,EST,2015,1.755649563,7.289082191,58.595272,25.013607,233
Estonia,EST,2016,1.617479169,6.264842987,58.595272,25.013607,233
Estonia,EST,2017,1.502637656,5.596156851,58.595272,25.013607,233
Estonia,EST,2018,1.440540019,5.670385746,58.595272,25.013607,233
Estonia,EST,2019,1.40052576,5.896921066,58.595272,25.013607,233
Eswatini,SWZ,1990,179.7465741,33.61448834,-26.522503,31.465866,748
Eswatini,SWZ,1991,174.3735735,35.03384057,-26.522503,31.465866,748
Eswatini,SWZ,1992,167.195984,35.72159113,-26.522503,31.465866,748
Eswatini,SWZ,1993,159.793971,36.2528334,-26.522503,31.465866,748
Eswatini,SWZ,1994,155.9281859,37.29368263,-26.522503,31.465866,748
Eswatini,SWZ,1995,155.3359355,39.01335834,-26.522503,31.465866,748
Eswatini,SWZ,1996,155.1726193,40.83568819,-26.522503,31.465866,748
Eswatini,SWZ,1997,152.0887415,41.74193183,-26.522503,31.465866,748
Eswatini,SWZ,1998,153.4059901,43.75384798,-26.522503,31.465866,748
Eswatini,SWZ,1999,155.2383965,45.86581705,-26.522503,31.465866,748
Eswatini,SWZ,2000,161.2541201,48.81454757,-26.522503,31.465866,748
Eswatini,SWZ,2001,164.7358223,51.42881891,-26.522503,31.465866,748
Eswatini,SWZ,2002,167.7013646,53.62251749,-26.522503,31.465866,748
Eswatini,SWZ,2003,167.801864,55.46908819,-26.522503,31.465866,748
Eswatini,SWZ,2004,167.640106,57.8582672,-26.522503,31.465866,748
Eswatini,SWZ,2005,166.0560319,59.91167552,-26.522503,31.465866,748
Eswatini,SWZ,2006,160.5424223,61.38009271,-26.522503,31.465866,748
Eswatini,SWZ,2007,155.7265388,61.86119612,-26.522503,31.465866,748
Eswatini,SWZ,2008,150.8701455,62.74680338,-26.522503,31.465866,748
Eswatini,SWZ,2009,145.5670817,63.2025671,-26.522503,31.465866,748
Eswatini,SWZ,2010,138.0191304,62.67857599,-26.522503,31.465866,748
Eswatini,SWZ,2011,129.7475402,62.57589035,-26.522503,31.465866,748
Eswatini,SWZ,2012,123.4759263,63.21374517,-26.522503,31.465866,748
Eswatini,SWZ,2013,116.9343812,64.09411374,-26.522503,31.465866,748
Eswatini,SWZ,2014,110.2757969,62.13524073,-26.522503,31.465866,748
Eswatini,SWZ,2015,104.2157426,61.2504089,-26.522503,31.465866,748
Eswatini,SWZ,2016,98.55543791,60.88382245,-26.522503,31.465866,748
Eswatini,SWZ,2017,93.46271008,61.30706928,-26.522503,31.465866,748
Eswatini,SWZ,2018,89.31035574,62.04606118,-26.522503,31.465866,748
Eswatini,SWZ,2019,85.76490974,62.67333508,-26.522503,31.465866,748
Ethiopia,ETH,1990,326.5119586,13.94579865,9.145,40.489673,231
Ethiopia,ETH,1991,321.502179,13.56494182,9.145,40.489673,231
Ethiopia,ETH,1992,319.1880024,13.39221499,9.145,40.489673,231
Ethiopia,ETH,1993,312.9772208,13.18889488,9.145,40.489673,231
Ethiopia,ETH,1994,305.9711457,13.00512405,9.145,40.489673,231
Ethiopia,ETH,1995,299.6122365,12.85334527,9.145,40.489673,231
Ethiopia,ETH,1996,290.8406796,12.54323071,9.145,40.489673,231
Ethiopia,ETH,1997,283.7870566,12.77096736,9.145,40.489673,231
Ethiopia,ETH,1998,278.120005,13.12811451,9.145,40.489673,231
Ethiopia,ETH,1999,271.5531718,13.55098624,9.145,40.489673,231
Ethiopia,ETH,2000,261.548944,13.17293984,9.145,40.489673,231
Ethiopia,ETH,2001,251.1210533,12.87183377,9.145,40.489673,231
Ethiopia,ETH,2002,242.8852073,12.64364736,9.145,40.489673,231
Ethiopia,ETH,2003,234.9326421,12.68902708,9.145,40.489673,231
Ethiopia,ETH,2004,227.0221635,12.82795764,9.145,40.489673,231
Ethiopia,ETH,2005,219.9140182,13.22014525,9.145,40.489673,231
Ethiopia,ETH,2006,210.6380195,13.94575505,9.145,40.489673,231
Ethiopia,ETH,2007,200.9863654,14.48615329,9.145,40.489673,231
Ethiopia,ETH,2008,191.2798586,14.70760996,9.145,40.489673,231
Ethiopia,ETH,2009,181.8940339,14.91429924,9.145,40.489673,231
Ethiopia,ETH,2010,173.2286751,15.42377209,9.145,40.489673,231
Ethiopia,ETH,2011,166.8829711,16.15375368,9.145,40.489673,231
Ethiopia,ETH,2012,160.6323942,16.79553672,9.145,40.489673,231
Ethiopia,ETH,2013,154.52789,17.36567703,9.145,40.489673,231
Ethiopia,ETH,2014,149.9383809,17.9021359,9.145,40.489673,231
Ethiopia,ETH,2015,144.9900035,18.54942899,9.145,40.489673,231
Ethiopia,ETH,2016,140.4046644,18.97872659,9.145,40.489673,231
Ethiopia,ETH,2017,136.743074,19.52217094,9.145,40.489673,231
Ethiopia,ETH,2018,133.5067331,20.34815104,9.145,40.489673,231
Ethiopia,ETH,2019,129.9507611,21.06998436,9.145,40.489673,231
Fiji,FJI,1990,140.5152709,23.44474038,-16.578193,179.414413,242
Fiji,FJI,1991,137.6471957,23.96289017,-16.578193,179.414413,242
Fiji,FJI,1992,134.0964295,24.68267461,-16.578193,179.414413,242
Fiji,FJI,1993,131.6472314,25.78644826,-16.578193,179.414413,242
Fiji,FJI,1994,128.9313247,27.0535332,-16.578193,179.414413,242
Fiji,FJI,1995,126.5869024,28.52209773,-16.578193,179.414413,242
Fiji,FJI,1996,124.0857585,31.24610431,-16.578193,179.414413,242
Fiji,FJI,1997,119.6183776,35.15713012,-16.578193,179.414413,242
Fiji,FJI,1998,111.6591669,38.27109206,-16.578193,179.414413,242
Fiji,FJI,1999,112.0672436,43.8826775,-16.578193,179.414413,242
Fiji,FJI,2000,110.5214722,47.06681903,-16.578193,179.414413,242
Fiji,FJI,2001,103.4531562,46.51722256,-16.578193,179.414413,242
Fiji,FJI,2002,97.95493145,45.87448169,-16.578193,179.414413,242
Fiji,FJI,2003,96.0981487,46.75977223,-16.578193,179.414413,242
Fiji,FJI,2004,88.85070049,44.76414502,-16.578193,179.414413,242
Fiji,FJI,2005,86.16694969,44.86888908,-16.578193,179.414413,242
Fiji,FJI,2006,84.24199008,45.16331325,-16.578193,179.414413,242
Fiji,FJI,2007,83.27965633,45.72063684,-16.578193,179.414413,242
Fiji,FJI,2008,81.77787015,45.75950112,-16.578193,179.414413,242
Fiji,FJI,2009,77.50812066,44.34582724,-16.578193,179.414413,242
Fiji,FJI,2010,74.97781361,44.42893245,-16.578193,179.414413,242
Fiji,FJI,2011,72.23648717,44.60455246,-16.578193,179.414413,242
Fiji,FJI,2012,68.68596455,44.59035553,-16.578193,179.414413,242
Fiji,FJI,2013,65.03455278,44.66059268,-16.578193,179.414413,242
Fiji,FJI,2014,61.63654973,45.06198865,-16.578193,179.414413,242
Fiji,FJI,2015,58.26090775,45.41572354,-16.578193,179.414413,242
Fiji,FJI,2016,54.62115919,46.74549509,-16.578193,179.414413,242
Fiji,FJI,2017,51.11515454,48.03995559,-16.578193,179.414413,242
Fiji,FJI,2018,47.91547913,48.54546246,-16.578193,179.414413,242
Fiji,FJI,2019,44.90041296,48.61884836,-16.578193,179.414413,242
Finland,FIN,1990,0.356043411,19.29913816,61.92411,25.748151,246
Finland,FIN,1991,0.317346281,18.19614956,61.92411,25.748151,246
Finland,FIN,1992,0.287558933,17.42604763,61.92411,25.748151,246
Finland,FIN,1993,0.258629525,16.58160234,61.92411,25.748151,246
Finland,FIN,1994,0.225193505,15.17927031,61.92411,25.748151,246
Finland,FIN,1995,0.204594976,14.59544416,61.92411,25.748151,246
Finland,FIN,1996,0.184378585,13.80961586,61.92411,25.748151,246
Finland,FIN,1997,0.167616835,13.1250966,61.92411,25.748151,246
Finland,FIN,1998,0.15097707,12.35706738,61.92411,25.748151,246
Finland,FIN,1999,0.136282171,11.63108506,61.92411,25.748151,246
Finland,FIN,2000,0.122797058,10.95762797,61.92411,25.748151,246
Finland,FIN,2001,0.108683874,10.23904078,61.92411,25.748151,246
Finland,FIN,2002,0.097487952,9.740887089,61.92411,25.748151,246
Finland,FIN,2003,0.086301793,9.192060993,61.92411,25.748151,246
Finland,FIN,2004,0.076225332,8.605074944,61.92411,25.748151,246
Finland,FIN,2005,0.067540557,8.175236434,61.92411,25.748151,246
Finland,FIN,2006,0.060406394,7.749177969,61.92411,25.748151,246
Finland,FIN,2007,0.055547712,7.571344291,61.92411,25.748151,246
Finland,FIN,2008,0.05081625,7.30757565,61.92411,25.748151,246
Finland,FIN,2009,0.04665596,7.180943202,61.92411,25.748151,246
Finland,FIN,2010,0.042412325,6.981018912,61.92411,25.748151,246
Finland,FIN,2011,0.03752687,6.447611202,61.92411,25.748151,246
Finland,FIN,2012,0.032892543,5.73365837,61.92411,25.748151,246
Finland,FIN,2013,0.028260721,4.858605966,61.92411,25.748151,246
Finland,FIN,2014,0.02419449,4.029340474,61.92411,25.748151,246
Finland,FIN,2015,0.020818099,3.364264196,61.92411,25.748151,246
Finland,FIN,2016,0.018216916,2.896796357,61.92411,25.748151,246
Finland,FIN,2017,0.01691683,2.646540611,61.92411,25.748151,246
Finland,FIN,2018,0.016868051,2.807412296,61.92411,25.748151,246
Finland,FIN,2019,0.017379291,3.125154137,61.92411,25.748151,246
France,FRA,1990,0.251174846,28.33879336,46.227638,2.213749,250
France,FRA,1991,0.227765482,27.08492569,46.227638,2.213749,250
France,FRA,1992,0.206113369,25.78549896,46.227638,2.213749,250
France,FRA,1993,0.18874202,25.01328722,46.227638,2.213749,250
France,FRA,1994,0.17120987,24.08383653,46.227638,2.213749,250
France,FRA,1995,0.159239856,23.74208996,46.227638,2.213749,250
France,FRA,1996,0.148493485,23.26013407,46.227638,2.213749,250
France,FRA,1997,0.136600816,22.3825286,46.227638,2.213749,250
France,FRA,1998,0.128464115,22.02245561,46.227638,2.213749,250
France,FRA,1999,0.119167886,21.23646482,46.227638,2.213749,250
France,FRA,2000,0.109006513,20.31393048,46.227638,2.213749,250
France,FRA,2001,0.100278381,19.57175935,46.227638,2.213749,250
France,FRA,2002,0.092372952,19.20146212,46.227638,2.213749,250
France,FRA,2003,0.084357292,18.48790708,46.227638,2.213749,250
France,FRA,2004,0.07377676,17.13096099,46.227638,2.213749,250
France,FRA,2005,0.067315632,16.51290934,46.227638,2.213749,250
France,FRA,2006,0.060932035,15.94572548,46.227638,2.213749,250
France,FRA,2007,0.055313094,15.57403978,46.227638,2.213749,250
France,FRA,2008,0.050809662,15.37304277,46.227638,2.213749,250
France,FRA,2009,0.046790516,15.2531217,46.227638,2.213749,250
France,FRA,2010,0.042942513,14.89921031,46.227638,2.213749,250
France,FRA,2011,0.03981614,14.30884098,46.227638,2.213749,250
France,FRA,2012,0.037275572,13.54948636,46.227638,2.213749,250
France,FRA,2013,0.034513477,12.52636553,46.227638,2.213749,250
France,FRA,2014,0.031717358,11.44372319,46.227638,2.213749,250
France,FRA,2015,0.030250735,10.86127678,46.227638,2.213749,250
France,FRA,2016,0.027640654,9.840775057,46.227638,2.213749,250
France,FRA,2017,0.02614977,9.405720274,46.227638,2.213749,250
France,FRA,2018,0.024775772,9.382478149,46.227638,2.213749,250
France,FRA,2019,0.023705893,9.366561679,46.227638,2.213749,250
Gabon,GAB,1990,136.3699877,47.83450326,-0.803689,11.609444,266
Gabon,GAB,1991,126.908799,49.72189876,-0.803689,11.609444,266
Gabon,GAB,1992,118.307702,51.86597268,-0.803689,11.609444,266
Gabon,GAB,1993,110.1905146,54.0795895,-0.803689,11.609444,266
Gabon,GAB,1994,103.9591694,57.12865219,-0.803689,11.609444,266
Gabon,GAB,1995,98.38146108,60.76373876,-0.803689,11.609444,266
Gabon,GAB,1996,92.06138731,64.14049331,-0.803689,11.609444,266
Gabon,GAB,1997,84.22644196,66.87338365,-0.803689,11.609444,266
Gabon,GAB,1998,77.34921449,69.92859656,-0.803689,11.609444,266
Gabon,GAB,1999,71.27811363,72.71753663,-0.803689,11.609444,266
Gabon,GAB,2000,66.54646539,75.46949062,-0.803689,11.609444,266
Gabon,GAB,2001,61.93984919,76.93482893,-0.803689,11.609444,266
Gabon,GAB,2002,56.681546,76.81043377,-0.803689,11.609444,266
Gabon,GAB,2003,52.94217047,78.14126877,-0.803689,11.609444,266
Gabon,GAB,2004,49.05975445,79.12063967,-0.803689,11.609444,266
Gabon,GAB,2005,44.56830704,79.25784299,-0.803689,11.609444,266
Gabon,GAB,2006,40.89868259,80.71246554,-0.803689,11.609444,266
Gabon,GAB,2007,36.96573332,81.49045378,-0.803689,11.609444,266
Gabon,GAB,2008,33.70019038,83.20825308,-0.803689,11.609444,266
Gabon,GAB,2009,29.9965545,83.66382638,-0.803689,11.609444,266
Gabon,GAB,2010,26.35167166,83.57870648,-0.803689,11.609444,266
Gabon,GAB,2011,23.22548856,85.42722684,-0.803689,11.609444,266
Gabon,GAB,2012,19.87525787,86.82464093,-0.803689,11.609444,266
Gabon,GAB,2013,16.80045334,88.08741055,-0.803689,11.609444,266
Gabon,GAB,2014,14.29444765,89.33712266,-0.803689,11.609444,266
Gabon,GAB,2015,12.38855186,89.91472873,-0.803689,11.609444,266
Gabon,GAB,2016,10.89524131,86.68486175,-0.803689,11.609444,266
Gabon,GAB,2017,9.645993987,83.74367071,-0.803689,11.609444,266
Gabon,GAB,2018,8.3997572,84.23707703,-0.803689,11.609444,266
Gabon,GAB,2019,7.211783637,85.99621018,-0.803689,11.609444,266
Gambia,GMB,1990,214.1947716,23.85623067,13.443182,-15.310139,270
Gambia,GMB,1991,211.1737729,24.30295848,13.443182,-15.310139,270
Gambia,GMB,1992,210.3230869,25.00978092,13.443182,-15.310139,270
Gambia,GMB,1993,202.6415368,24.8534995,13.443182,-15.310139,270
Gambia,GMB,1994,198.2211043,25.11354314,13.443182,-15.310139,270
Gambia,GMB,1995,203.8477032,26.78792637,13.443182,-15.310139,270
Gambia,GMB,1996,192.4205706,26.2813561,13.443182,-15.310139,270
Gambia,GMB,1997,189.5214881,27.13131832,13.443182,-15.310139,270
Gambia,GMB,1998,190.3975359,28.56071789,13.443182,-15.310139,270
Gambia,GMB,1999,193.7359971,30.32483927,13.443182,-15.310139,270
Gambia,GMB,2000,184.4295448,29.60354946,13.443182,-15.310139,270
Gambia,GMB,2001,178.6681852,29.39160366,13.443182,-15.310139,270
Gambia,GMB,2002,179.1693644,30.19039113,13.443182,-15.310139,270
Gambia,GMB,2003,178.9416448,31.04019719,13.443182,-15.310139,270
Gambia,GMB,2004,186.3205133,33.36532917,13.443182,-15.310139,270
Gambia,GMB,2005,186.0174446,34.51182018,13.443182,-15.310139,270
Gambia,GMB,2006,181.6404172,35.06610743,13.443182,-15.310139,270
Gambia,GMB,2007,178.4492826,35.58056883,13.443182,-15.310139,270
Gambia,GMB,2008,172.038921,35.20981162,13.443182,-15.310139,270
Gambia,GMB,2009,170.1574486,36.12828014,13.443182,-15.310139,270
Gambia,GMB,2010,165.4950876,36.85414463,13.443182,-15.310139,270
Gambia,GMB,2011,155.0717172,36.5875823,13.443182,-15.310139,270
Gambia,GMB,2012,152.4070462,38.46898869,13.443182,-15.310139,270
Gambia,GMB,2013,150.6439833,41.12748304,13.443182,-15.310139,270
Gambia,GMB,2014,152.666151,44.65499193,13.443182,-15.310139,270
Gambia,GMB,2015,147.2928249,45.55249592,13.443182,-15.310139,270
Gambia,GMB,2016,147.64907,47.54169216,13.443182,-15.310139,270
Gambia,GMB,2017,149.4551438,49.68460117,13.443182,-15.310139,270
Gambia,GMB,2018,146.2499792,50.12820088,13.443182,-15.310139,270
Gambia,GMB,2019,144.2414678,50.15409699,13.443182,-15.310139,270
Georgia,GEO,1990,85.48763018,75.47492373,42.315407,43.356892,268
Georgia,GEO,1991,84.55848921,76.51432495,42.315407,43.356892,268
Georgia,GEO,1992,84.19142254,77.53463497,42.315407,43.356892,268
Georgia,GEO,1993,80.70734347,75.17675946,42.315407,43.356892,268
Georgia,GEO,1994,80.11724583,75.13082129,42.315407,43.356892,268
Georgia,GEO,1995,72.16226754,68.15076413,42.315407,43.356892,268
Georgia,GEO,1996,67.66692663,63.00475446,42.315407,43.356892,268
Georgia,GEO,1997,69.27742301,62.14776981,42.315407,43.356892,268
Georgia,GEO,1998,71.94413748,61.70217901,42.315407,43.356892,268
Georgia,GEO,1999,74.25209224,61.09476669,42.315407,43.356892,268
Georgia,GEO,2000,75.59056567,61.04634298,42.315407,43.356892,268
Georgia,GEO,2001,73.8604173,60.24516903,42.315407,43.356892,268
Georgia,GEO,2002,74.39819797,62.39644843,42.315407,43.356892,268
Georgia,GEO,2003,72.45535394,62.83961296,42.315407,43.356892,268
Georgia,GEO,2004,69.47351408,62.54738011,42.315407,43.356892,268
Georgia,GEO,2005,65.30221101,60.69744045,42.315407,43.356892,268
Georgia,GEO,2006,60.58979253,58.86160869,42.315407,43.356892,268
Georgia,GEO,2007,54.81701014,56.34967663,42.315407,43.356892,268
Georgia,GEO,2008,51.70099647,56.1384047,42.315407,43.356892,268
Georgia,GEO,2009,50.47265319,57.46856031,42.315407,43.356892,268
Georgia,GEO,2010,47.70138871,57.22445482,42.315407,43.356892,268
Georgia,GEO,2011,43.86343765,55.869025,42.315407,43.356892,268
Georgia,GEO,2012,39.087751,53.3001504,42.315407,43.356892,268
Georgia,GEO,2013,35.06453786,51.38699527,42.315407,43.356892,268
Georgia,GEO,2014,32.25606958,50.51894898,42.315407,43.356892,268
Georgia,GEO,2015,30.31317073,50.46485222,42.315407,43.356892,268
Georgia,GEO,2016,29.65634375,52.21940373,42.315407,43.356892,268
Georgia,GEO,2017,28.28962271,52.36976156,42.315407,43.356892,268
Georgia,GEO,2018,27.05701187,52.5012229,42.315407,43.356892,268
Georgia,GEO,2019,25.90365756,52.51354792,42.315407,43.356892,268
Germany,DEU,1990,0.098507362,49.89918538,51.165691,10.451526,276
Germany,DEU,1991,0.089939207,47.89609927,51.165691,10.451526,276
Germany,DEU,1992,0.081702541,45.54596171,51.165691,10.451526,276
Germany,DEU,1993,0.07588186,44.18414423,51.165691,10.451526,276
Germany,DEU,1994,0.069933194,42.08006491,51.165691,10.451526,276
Germany,DEU,1995,0.065239811,40.05522636,51.165691,10.451526,276
Germany,DEU,1996,0.061569086,37.98430277,51.165691,10.451526,276
Germany,DEU,1997,0.05786782,35.55815628,51.165691,10.451526,276
Germany,DEU,1998,0.054367384,33.28472919,51.165691,10.451526,276
Germany,DEU,1999,0.050851367,30.99907568,51.165691,10.451526,276
Germany,DEU,2000,0.047056498,28.87008375,51.165691,10.451526,276
Germany,DEU,2001,0.043840926,27.17394399,51.165691,10.451526,276
Germany,DEU,2002,0.041563231,26.49307619,51.165691,10.451526,276
Germany,DEU,2003,0.038964556,25.47398168,51.165691,10.451526,276
Germany,DEU,2004,0.035081422,23.69811236,51.165691,10.451526,276
Germany,DEU,2005,0.032232396,22.55329355,51.165691,10.451526,276
Germany,DEU,2006,0.029715582,22.02206033,51.165691,10.451526,276
Germany,DEU,2007,0.027511862,22.00675265,51.165691,10.451526,276
Germany,DEU,2008,0.02548828,21.99913825,51.165691,10.451526,276
Germany,DEU,2009,0.023558435,21.96406554,51.165691,10.451526,276
Germany,DEU,2010,0.021827562,21.50728342,51.165691,10.451526,276
Germany,DEU,2011,0.020570835,20.65883079,51.165691,10.451526,276
Germany,DEU,2012,0.019627648,19.49700635,51.165691,10.451526,276
Germany,DEU,2013,0.018998032,18.31082552,51.165691,10.451526,276
Germany,DEU,2014,0.01786557,16.74851999,51.165691,10.451526,276
Germany,DEU,2015,0.017456376,16.07671565,51.165691,10.451526,276
Germany,DEU,2016,0.016544051,15.11259626,51.165691,10.451526,276
Germany,DEU,2017,0.015562259,14.31323623,51.165691,10.451526,276
Germany,DEU,2018,0.014811294,14.20273842,51.165691,10.451526,276
Germany,DEU,2019,0.014121999,14.09913514,51.165691,10.451526,276
Ghana,GHA,1990,171.9028971,44.62396336,7.946527,-1.023194,288
Ghana,GHA,1991,168.3546327,43.91319013,7.946527,-1.023194,288
Ghana,GHA,1992,165.2988066,43.48261482,7.946527,-1.023194,288
Ghana,GHA,1993,160.9249067,42.98216569,7.946527,-1.023194,288
Ghana,GHA,1994,156.9262373,42.65784997,7.946527,-1.023194,288
Ghana,GHA,1995,153.2464773,42.51327683,7.946527,-1.023194,288
Ghana,GHA,1996,150.7938164,44.13935116,7.946527,-1.023194,288
Ghana,GHA,1997,149.0059284,47.84038329,7.946527,-1.023194,288
Ghana,GHA,1998,144.636093,51.33893744,7.946527,-1.023194,288
Ghana,GHA,1999,141.4473715,54.63683713,7.946527,-1.023194,288
Ghana,GHA,2000,139.350508,56.45419789,7.946527,-1.023194,288
Ghana,GHA,2001,138.1046956,57.40313328,7.946527,-1.023194,288
Ghana,GHA,2002,137.681706,58.26233293,7.946527,-1.023194,288
Ghana,GHA,2003,135.8248941,58.57645272,7.946527,-1.023194,288
Ghana,GHA,2004,134.3731746,59.26238804,7.946527,-1.023194,288
Ghana,GHA,2005,132.8197108,60.49153659,7.946527,-1.023194,288
Ghana,GHA,2006,131.2269048,62.44303181,7.946527,-1.023194,288
Ghana,GHA,2007,127.990851,63.50531255,7.946527,-1.023194,288
Ghana,GHA,2008,123.5623451,64.06021012,7.946527,-1.023194,288
Ghana,GHA,2009,119.1246024,64.92423855,7.946527,-1.023194,288
Ghana,GHA,2010,114.6506199,66.58393252,7.946527,-1.023194,288
Ghana,GHA,2011,109.7652762,69.39213202,7.946527,-1.023194,288
Ghana,GHA,2012,103.5318363,72.7897161,7.946527,-1.023194,288
Ghana,GHA,2013,97.44049875,76.50874964,7.946527,-1.023194,288
Ghana,GHA,2014,91.526072,79.42767276,7.946527,-1.023194,288
Ghana,GHA,2015,87.31047617,81.94112148,7.946527,-1.023194,288
Ghana,GHA,2016,82.57817099,81.91045435,7.946527,-1.023194,288
Ghana,GHA,2017,78.27152593,82.00205465,7.946527,-1.023194,288
Ghana,GHA,2018,73.47365465,82.04474492,7.946527,-1.023194,288
Ghana,GHA,2019,69.71186609,82.34041503,7.946527,-1.023194,288
Greece,GRC,1990,2.098800595,48.14036758,39.074208,21.824312,300
Greece,GRC,1991,1.883007288,47.49202704,39.074208,21.824312,300
Greece,GRC,1992,1.693655784,47.31672853,39.074208,21.824312,300
Greece,GRC,1993,1.493313943,46.27257081,39.074208,21.824312,300
Greece,GRC,1994,1.336061294,45.90220236,39.074208,21.824312,300
Greece,GRC,1995,1.205399005,45.65415026,39.074208,21.824312,300
Greece,GRC,1996,1.082364193,45.22089711,39.074208,21.824312,300
Greece,GRC,1997,0.966690411,45.12761207,39.074208,21.824312,300
Greece,GRC,1998,0.880272952,45.64479342,39.074208,21.824312,300
Greece,GRC,1999,0.797689651,45.93087981,39.074208,21.824312,300
Greece,GRC,2000,0.717339148,45.2456435,39.074208,21.824312,300
Greece,GRC,2001,0.644893613,44.27519555,39.074208,21.824312,300
Greece,GRC,2002,0.584063499,43.37560987,39.074208,21.824312,300
Greece,GRC,2003,0.529754315,41.98360557,39.074208,21.824312,300
Greece,GRC,2004,0.476117337,40.24220406,39.074208,21.824312,300
Greece,GRC,2005,0.426352803,38.44641167,39.074208,21.824312,300
Greece,GRC,2006,0.38308142,37.61845232,39.074208,21.824312,300
Greece,GRC,2007,0.353134601,37.94169297,39.074208,21.824312,300
Greece,GRC,2008,0.312242322,36.44679704,39.074208,21.824312,300
Greece,GRC,2009,0.281900962,35.552266,39.074208,21.824312,300
Greece,GRC,2010,0.255356558,34.15713385,39.074208,21.824312,300
Greece,GRC,2011,0.238878582,33.35326979,39.074208,21.824312,300
Greece,GRC,2012,0.224666018,32.11622382,39.074208,21.824312,300
Greece,GRC,2013,0.204839463,29.56481324,39.074208,21.824312,300
Greece,GRC,2014,0.18913594,27.21145071,39.074208,21.824312,300
Greece,GRC,2015,0.179529951,25.76479576,39.074208,21.824312,300
Greece,GRC,2016,0.170062438,23.85284545,39.074208,21.824312,300
Greece,GRC,2017,0.163470118,22.84023318,39.074208,21.824312,300
Greece,GRC,2018,0.159359653,23.05260162,39.074208,21.824312,300
Greece,GRC,2019,0.152015028,23.1288969,39.074208,21.824312,300
Greenland,GRL,1990,7.257019728,25.2404542,71.706936,-42.604303,304
Greenland,GRL,1991,7.132618353,24.78939671,71.706936,-42.604303,304
Greenland,GRL,1992,6.97042201,24.52177914,71.706936,-42.604303,304
Greenland,GRL,1993,7.33228769,26.32473778,71.706936,-42.604303,304
Greenland,GRL,1994,7.191343054,26.73292732,71.706936,-42.604303,304
Greenland,GRL,1995,6.965872488,26.82918894,71.706936,-42.604303,304
Greenland,GRL,1996,6.628319406,25.98665124,71.706936,-42.604303,304
Greenland,GRL,1997,6.199168117,25.06958342,71.706936,-42.604303,304
Greenland,GRL,1998,5.668090728,23.42184011,71.706936,-42.604303,304
Greenland,GRL,1999,5.182849786,22.06969706,71.706936,-42.604303,304
Greenland,GRL,2000,4.668432636,20.89749748,71.706936,-42.604303,304
Greenland,GRL,2001,4.143313971,20.41449519,71.706936,-42.604303,304
Greenland,GRL,2002,3.616433602,20.55835742,71.706936,-42.604303,304
Greenland,GRL,2003,2.982160638,19.72926602,71.706936,-42.604303,304
Greenland,GRL,2004,2.331653743,17.57669544,71.706936,-42.604303,304
Greenland,GRL,2005,2.009594291,16.97557141,71.706936,-42.604303,304
Greenland,GRL,2006,1.742697707,15.92941285,71.706936,-42.604303,304
Greenland,GRL,2007,1.501759008,15.21792002,71.706936,-42.604303,304
Greenland,GRL,2008,1.289889029,14.47144027,71.706936,-42.604303,304
Greenland,GRL,2009,1.116841269,14.16645643,71.706936,-42.604303,304
Greenland,GRL,2010,0.995055919,13.74494493,71.706936,-42.604303,304
Greenland,GRL,2011,0.90900954,13.33495358,71.706936,-42.604303,304
Greenland,GRL,2012,0.838657833,13.13716562,71.706936,-42.604303,304
Greenland,GRL,2013,0.78101037,13.02135396,71.706936,-42.604303,304
Greenland,GRL,2014,0.732960069,12.72144153,71.706936,-42.604303,304
Greenland,GRL,2015,0.693262463,11.99677552,71.706936,-42.604303,304
Greenland,GRL,2016,0.666176394,12.02155523,71.706936,-42.604303,304
Greenland,GRL,2017,0.642128787,11.95088658,71.706936,-42.604303,304
Greenland,GRL,2018,0.607292897,12.22184331,71.706936,-42.604303,304
Greenland,GRL,2019,0.558868025,11.62319636,71.706936,-42.604303,304
Grenada,GRD,1990,64.42352321,46.50198859,12.262776,-61.604171,308
Grenada,GRD,1991,55.13260436,48.71278245,12.262776,-61.604171,308
Grenada,GRD,1992,48.01081617,51.73847307,12.262776,-61.604171,308
Grenada,GRD,1993,42.15039312,55.01811559,12.262776,-61.604171,308
Grenada,GRD,1994,35.40878098,56.09556864,12.262776,-61.604171,308
Grenada,GRD,1995,29.48398861,56.16230631,12.262776,-61.604171,308
Grenada,GRD,1996,24.16391882,55.31612855,12.262776,-61.604171,308
Grenada,GRD,1997,19.86859347,55.24039411,12.262776,-61.604171,308
Grenada,GRD,1998,16.40028029,55.4224678,12.262776,-61.604171,308
Grenada,GRD,1999,13.82604924,57.1108353,12.262776,-61.604171,308
Grenada,GRD,2000,11.85508796,57.00890051,12.262776,-61.604171,308
Grenada,GRD,2001,10.31037467,56.38373555,12.262776,-61.604171,308
Grenada,GRD,2002,8.985724979,55.30130519,12.262776,-61.604171,308
Grenada,GRD,2003,7.833493736,54.00848341,12.262776,-61.604171,308
Grenada,GRD,2004,6.942635422,52.84872334,12.262776,-61.604171,308
Grenada,GRD,2005,6.222124358,51.49450325,12.262776,-61.604171,308
Grenada,GRD,2006,5.720884843,50.84676318,12.262776,-61.604171,308
Grenada,GRD,2007,5.338966399,50.70370136,12.262776,-61.604171,308
Grenada,GRD,2008,5.066677305,51.19307183,12.262776,-61.604171,308
Grenada,GRD,2009,4.83146791,51.72225038,12.262776,-61.604171,308
Grenada,GRD,2010,4.566101503,52.04843518,12.262776,-61.604171,308
Grenada,GRD,2011,4.26040901,51.91145854,12.262776,-61.604171,308
Grenada,GRD,2012,3.828598168,49.73995006,12.262776,-61.604171,308
Grenada,GRD,2013,3.614444733,50.97312865,12.262776,-61.604171,308
Grenada,GRD,2014,3.411081964,51.95855001,12.262776,-61.604171,308
Grenada,GRD,2015,3.178345519,51.88942588,12.262776,-61.604171,308
Grenada,GRD,2016,3.079219218,52.68617165,12.262776,-61.604171,308
Grenada,GRD,2017,2.831692621,50.80955622,12.262776,-61.604171,308
Grenada,GRD,2018,2.610345973,50.68729431,12.262776,-61.604171,308
Grenada,GRD,2019,2.393528578,51.05134236,12.262776,-61.604171,308
Guam,GUM,1990,6.296261598,25.53305322,13.444304,144.793731,316
Guam,GUM,1991,6.106574244,25.56378329,13.444304,144.793731,316
Guam,GUM,1992,5.784195213,25.08662632,13.444304,144.793731,316
Guam,GUM,1993,5.360027869,24.20277603,13.444304,144.793731,316
Guam,GUM,1994,4.843182152,22.920255,13.444304,144.793731,316
Guam,GUM,1995,4.320036823,21.08428754,13.444304,144.793731,316
Guam,GUM,1996,3.890263963,19.65734699,13.444304,144.793731,316
Guam,GUM,1997,3.574488095,18.64304814,13.444304,144.793731,316
Guam,GUM,1998,3.310649346,17.75421583,13.444304,144.793731,316
Guam,GUM,1999,3.113133251,16.99092892,13.444304,144.793731,316
Guam,GUM,2000,2.986629689,16.60221038,13.444304,144.793731,316
Guam,GUM,2001,2.901294527,16.40360449,13.444304,144.793731,316
Guam,GUM,2002,2.8119448,16.17179885,13.444304,144.793731,316
Guam,GUM,2003,2.689612847,15.61596405,13.444304,144.793731,316
Guam,GUM,2004,2.488268529,14.70718941,13.444304,144.793731,316
Guam,GUM,2005,2.281507379,13.6281488,13.444304,144.793731,316
Guam,GUM,2006,2.279401367,13.3488763,13.444304,144.793731,316
Guam,GUM,2007,2.293813197,12.98752841,13.444304,144.793731,316
Guam,GUM,2008,2.359209877,12.82766097,13.444304,144.793731,316
Guam,GUM,2009,2.454067393,12.83361506,13.444304,144.793731,316
Guam,GUM,2010,2.497581656,12.70997168,13.444304,144.793731,316
Guam,GUM,2011,2.52713288,13.33656956,13.444304,144.793731,316
Guam,GUM,2012,2.671409415,15.57470793,13.444304,144.793731,316
Guam,GUM,2013,2.845942517,18.45715649,13.444304,144.793731,316
Guam,GUM,2014,2.972182398,20.86928564,13.444304,144.793731,316
Guam,GUM,2015,3.03011851,21.8682866,13.444304,144.793731,316
Guam,GUM,2016,2.797288272,18.38129422,13.444304,144.793731,316
Guam,GUM,2017,2.539881349,14.96813819,13.444304,144.793731,316
Guam,GUM,2018,2.477603584,15.19486114,13.444304,144.793731,316
Guam,GUM,2019,2.483053296,16.67873768,13.444304,144.793731,316
Guatemala,GTM,1990,177.1226147,33.90704722,15.783471,-90.230759,320
Guatemala,GTM,1991,181.7549406,37.59417449,15.783471,-90.230759,320
Guatemala,GTM,1992,183.5816635,40.8135927,15.783471,-90.230759,320
Guatemala,GTM,1993,182.2240385,43.05444881,15.783471,-90.230759,320
Guatemala,GTM,1994,174.921227,43.62899109,15.783471,-90.230759,320
Guatemala,GTM,1995,157.6251067,41.1350382,15.783471,-90.230759,320
Guatemala,GTM,1996,147.9891308,40.17242489,15.783471,-90.230759,320
Guatemala,GTM,1997,148.5111999,42.29927736,15.783471,-90.230759,320
Guatemala,GTM,1998,147.2349157,43.79055288,15.783471,-90.230759,320
Guatemala,GTM,1999,139.3817519,43.33406257,15.783471,-90.230759,320
Guatemala,GTM,2000,132.3472863,41.55676951,15.783471,-90.230759,320
Guatemala,GTM,2001,124.857032,39.9462875,15.783471,-90.230759,320
Guatemala,GTM,2002,116.1590169,37.13048351,15.783471,-90.230759,320
Guatemala,GTM,2003,110.2456265,35.42558481,15.783471,-90.230759,320
Guatemala,GTM,2004,106.0468868,34.30324861,15.783471,-90.230759,320
Guatemala,GTM,2005,101.1823886,33.04553159,15.783471,-90.230759,320
Guatemala,GTM,2006,95.92949746,32.39246317,15.783471,-90.230759,320
Guatemala,GTM,2007,89.96707548,31.48768111,15.783471,-90.230759,320
Guatemala,GTM,2008,84.48811552,31.18886271,15.783471,-90.230759,320
Guatemala,GTM,2009,80.97662654,31.56992625,15.783471,-90.230759,320
Guatemala,GTM,2010,78.20881109,32.50472391,15.783471,-90.230759,320
Guatemala,GTM,2011,74.78556088,33.56154913,15.783471,-90.230759,320
Guatemala,GTM,2012,70.40244863,35.09402684,15.783471,-90.230759,320
Guatemala,GTM,2013,66.62636965,36.45754698,15.783471,-90.230759,320
Guatemala,GTM,2014,63.14618373,37.44998081,15.783471,-90.230759,320
Guatemala,GTM,2015,60.27294024,37.51380107,15.783471,-90.230759,320
Guatemala,GTM,2016,58.02152708,36.41981718,15.783471,-90.230759,320
Guatemala,GTM,2017,55.17849232,34.78312805,15.783471,-90.230759,320
Guatemala,GTM,2018,52.60353691,34.97016759,15.783471,-90.230759,320
Guatemala,GTM,2019,50.18841583,35.91711213,15.783471,-90.230759,320
Guinea,GIN,1990,268.5039071,22.22712467,9.945587,-9.696645,324
Guinea,GIN,1991,263.3484823,22.03938298,9.945587,-9.696645,324
Guinea,GIN,1992,260.4682419,21.97224014,9.945587,-9.696645,324
Guinea,GIN,1993,256.4097494,21.92389543,9.945587,-9.696645,324
Guinea,GIN,1994,253.2410583,21.91415426,9.945587,-9.696645,324
Guinea,GIN,1995,250.5397475,22.03359268,9.945587,-9.696645,324
Guinea,GIN,1996,246.9090202,22.470271,9.945587,-9.696645,324
Guinea,GIN,1997,242.2938378,23.22556745,9.945587,-9.696645,324
Guinea,GIN,1998,240.4490514,24.36887636,9.945587,-9.696645,324
Guinea,GIN,1999,238.9871081,25.23227901,9.945587,-9.696645,324
Guinea,GIN,2000,235.6287304,25.32581386,9.945587,-9.696645,324
Guinea,GIN,2001,231.8900809,25.52988567,9.945587,-9.696645,324
Guinea,GIN,2002,229.771191,25.80390798,9.945587,-9.696645,324
Guinea,GIN,2003,227.2559357,26.26827078,9.945587,-9.696645,324
Guinea,GIN,2004,227.6783114,27.04514681,9.945587,-9.696645,324
Guinea,GIN,2005,225.9786267,27.97146619,9.945587,-9.696645,324
Guinea,GIN,2006,225.6888082,29.14548387,9.945587,-9.696645,324
Guinea,GIN,2007,223.5285641,29.6448064,9.945587,-9.696645,324
Guinea,GIN,2008,221.2266691,29.67506004,9.945587,-9.696645,324
Guinea,GIN,2009,218.1447323,29.8178327,9.945587,-9.696645,324
Guinea,GIN,2010,217.1138149,30.8113722,9.945587,-9.696645,324
Guinea,GIN,2011,214.5414959,31.89718147,9.945587,-9.696645,324
Guinea,GIN,2012,212.1522284,33.17903552,9.945587,-9.696645,324
Guinea,GIN,2013,210.7348728,34.66236612,9.945587,-9.696645,324
Guinea,GIN,2014,208.9422238,35.78646498,9.945587,-9.696645,324
Guinea,GIN,2015,207.2846348,36.47866457,9.945587,-9.696645,324
Guinea,GIN,2016,202.9965511,36.1735348,9.945587,-9.696645,324
Guinea,GIN,2017,197.5125855,35.86892829,9.945587,-9.696645,324
Guinea,GIN,2018,192.559616,36.59699466,9.945587,-9.696645,324
Guinea,GIN,2019,184.9619436,36.73395688,9.945587,-9.696645,324
Guinea-Bissau,GNB,1990,317.6572729,30.22497369,11.803749,-15.180413,624
Guinea-Bissau,GNB,1991,312.5007116,30.43180999,11.803749,-15.180413,624
Guinea-Bissau,GNB,1992,307.9132146,30.69291509,11.803749,-15.180413,624
Guinea-Bissau,GNB,1993,303.2836451,30.95143547,11.803749,-15.180413,624
Guinea-Bissau,GNB,1994,299.0364995,31.27547922,11.803749,-15.180413,624
Guinea-Bissau,GNB,1995,294.6751869,31.64848291,11.803749,-15.180413,624
Guinea-Bissau,GNB,1996,290.8413297,32.35480876,11.803749,-15.180413,624
Guinea-Bissau,GNB,1997,284.6461454,33.08030793,11.803749,-15.180413,624
Guinea-Bissau,GNB,1998,279.8267359,34.04259928,11.803749,-15.180413,624
Guinea-Bissau,GNB,1999,275.4397771,34.65474752,11.803749,-15.180413,624
Guinea-Bissau,GNB,2000,271.9288337,34.65712504,11.803749,-15.180413,624
Guinea-Bissau,GNB,2001,269.3520177,34.79069072,11.803749,-15.180413,624
Guinea-Bissau,GNB,2002,268.2546753,35.04032508,11.803749,-15.180413,624
Guinea-Bissau,GNB,2003,266.4097837,35.40133252,11.803749,-15.180413,624
Guinea-Bissau,GNB,2004,266.6551941,36.21393186,11.803749,-15.180413,624
Guinea-Bissau,GNB,2005,262.7229332,36.83412567,11.803749,-15.180413,624
Guinea-Bissau,GNB,2006,259.5743337,37.80138358,11.803749,-15.180413,624
Guinea-Bissau,GNB,2007,258.5127444,38.61640744,11.803749,-15.180413,624
Guinea-Bissau,GNB,2008,254.7685167,38.65282106,11.803749,-15.180413,624
Guinea-Bissau,GNB,2009,250.7593151,39.08869699,11.803749,-15.180413,624
Guinea-Bissau,GNB,2010,246.0052907,39.93098379,11.803749,-15.180413,624
Guinea-Bissau,GNB,2011,240.3343832,41.01642329,11.803749,-15.180413,624
Guinea-Bissau,GNB,2012,234.5082278,42.16477561,11.803749,-15.180413,624
Guinea-Bissau,GNB,2013,229.4566679,43.89024776,11.803749,-15.180413,624
Guinea-Bissau,GNB,2014,224.7551237,45.46960821,11.803749,-15.180413,624
Guinea-Bissau,GNB,2015,219.9172338,46.67353882,11.803749,-15.180413,624
Guinea-Bissau,GNB,2016,214.9135265,47.33872484,11.803749,-15.180413,624
Guinea-Bissau,GNB,2017,209.6122257,47.49249087,11.803749,-15.180413,624
Guinea-Bissau,GNB,2018,203.5508803,47.30676661,11.803749,-15.180413,624
Guinea-Bissau,GNB,2019,198.9040149,46.65672764,11.803749,-15.180413,624
Guyana,GUY,1990,68.75223026,81.15288385,4.860416,-58.93018,328
Guyana,GUY,1991,63.47441769,77.39222703,4.860416,-58.93018,328
Guyana,GUY,1992,59.74387691,76.18470658,4.860416,-58.93018,328
Guyana,GUY,1993,60.93990242,81.5741835,4.860416,-58.93018,328
Guyana,GUY,1994,58.03531732,81.88652358,4.860416,-58.93018,328
Guyana,GUY,1995,56.07442237,83.93154665,4.860416,-58.93018,328
Guyana,GUY,1996,53.64143001,86.71106729,4.860416,-58.93018,328
Guyana,GUY,1997,49.35688528,88.22314127,4.860416,-58.93018,328
Guyana,GUY,1998,45.52909225,90.13617336,4.860416,-58.93018,328
Guyana,GUY,1999,40.25271533,86.97516897,4.860416,-58.93018,328
Guyana,GUY,2000,38.97945398,88.44009981,4.860416,-58.93018,328
Guyana,GUY,2001,38.27192769,88.05421348,4.860416,-58.93018,328
Guyana,GUY,2002,38.17331568,87.41917306,4.860416,-58.93018,328
Guyana,GUY,2003,37.50725374,85.03272849,4.860416,-58.93018,328
Guyana,GUY,2004,36.55604022,82.8678949,4.860416,-58.93018,328
Guyana,GUY,2005,34.58668085,80.04501967,4.860416,-58.93018,328
Guyana,GUY,2006,31.81808254,77.3295302,4.860416,-58.93018,328
Guyana,GUY,2007,29.69741146,77.40533597,4.860416,-58.93018,328
Guyana,GUY,2008,27.23134602,77.26475667,4.860416,-58.93018,328
Guyana,GUY,2009,24.24311069,75.66493151,4.860416,-58.93018,328
Guyana,GUY,2010,22.23328471,75.92622442,4.860416,-58.93018,328
Guyana,GUY,2011,20.09449496,75.59177186,4.860416,-58.93018,328
Guyana,GUY,2012,18.29900863,77.10289251,4.860416,-58.93018,328
Guyana,GUY,2013,16.45092396,77.98321207,4.860416,-58.93018,328
Guyana,GUY,2014,15.05518591,79.86824425,4.860416,-58.93018,328
Guyana,GUY,2015,13.5290775,79.08412029,4.860416,-58.93018,328
Guyana,GUY,2016,12.21179251,76.91407377,4.860416,-58.93018,328
Guyana,GUY,2017,11.13250221,74.36167061,4.860416,-58.93018,328
Guyana,GUY,2018,10.24253505,72.5112346,4.860416,-58.93018,328
Guyana,GUY,2019,9.411738496,70.21484117,4.860416,-58.93018,328
Haiti,HTI,1990,294.0437352,20.50068377,18.971187,-72.285215,332
Haiti,HTI,1991,285.6917055,20.16082447,18.971187,-72.285215,332
Haiti,HTI,1992,280.0042405,20.17124586,18.971187,-72.285215,332
Haiti,HTI,1993,274.8278471,20.07696212,18.971187,-72.285215,332
Haiti,HTI,1994,268.315448,20.13181122,18.971187,-72.285215,332
Haiti,HTI,1995,262.0767292,20.42649755,18.971187,-72.285215,332
Haiti,HTI,1996,253.538934,20.62935996,18.971187,-72.285215,332
Haiti,HTI,1997,247.2624976,21.30273949,18.971187,-72.285215,332
Haiti,HTI,1998,237.7163105,21.8439923,18.971187,-72.285215,332
Haiti,HTI,1999,232.8333456,22.92758992,18.971187,-72.285215,332
Haiti,HTI,2000,228.4499799,23.19134007,18.971187,-72.285215,332
Haiti,HTI,2001,225.2400832,24.0686738,18.971187,-72.285215,332
Haiti,HTI,2002,221.3312181,24.27439899,18.971187,-72.285215,332
Haiti,HTI,2003,219.0829296,24.80013052,18.971187,-72.285215,332
Haiti,HTI,2004,217.3541338,23.9048031,18.971187,-72.285215,332
Haiti,HTI,2005,215.5664171,23.51799732,18.971187,-72.285215,332
Haiti,HTI,2006,212.9727881,23.66915429,18.971187,-72.285215,332
Haiti,HTI,2007,210.3957511,23.85231112,18.971187,-72.285215,332
Haiti,HTI,2008,207.7411656,23.95413024,18.971187,-72.285215,332
Haiti,HTI,2009,204.9950793,23.76858731,18.971187,-72.285215,332
Haiti,HTI,2010,203.1123361,24.21093953,18.971187,-72.285215,332
Haiti,HTI,2011,203.3013426,25.42551701,18.971187,-72.285215,332
Haiti,HTI,2012,199.3055207,26.52260577,18.971187,-72.285215,332
Haiti,HTI,2013,195.6014415,27.41496453,18.971187,-72.285215,332
Haiti,HTI,2014,192.3308861,27.85630161,18.971187,-72.285215,332
Haiti,HTI,2015,189.3318675,28.02013413,18.971187,-72.285215,332
Haiti,HTI,2016,185.6197405,27.76111637,18.971187,-72.285215,332
Haiti,HTI,2017,181.4288495,27.44248325,18.971187,-72.285215,332
Haiti,HTI,2018,177.7728435,27.81333746,18.971187,-72.285215,332
Haiti,HTI,2019,173.445411,28.10262029,18.971187,-72.285215,332
Honduras,HND,1990,104.7462449,16.50430587,15.199999,-86.241905,340
Honduras,HND,1991,101.3556221,16.22380103,15.199999,-86.241905,340
Honduras,HND,1992,103.9679253,16.97142326,15.199999,-86.241905,340
Honduras,HND,1993,101.0447682,16.90550428,15.199999,-86.241905,340
Honduras,HND,1994,98.7199239,17.42615607,15.199999,-86.241905,340
Honduras,HND,1995,105.697762,19.28994426,15.199999,-86.241905,340
Honduras,HND,1996,109.9440742,21.13123742,15.199999,-86.241905,340
Honduras,HND,1997,106.5440409,21.90940826,15.199999,-86.241905,340
Honduras,HND,1998,102.9337934,23.30098106,15.199999,-86.241905,340
Honduras,HND,1999,99.63563148,24.9062267,15.199999,-86.241905,340
Honduras,HND,2000,96.57750399,25.5458722,15.199999,-86.241905,340
Honduras,HND,2001,94.08181953,26.50699066,15.199999,-86.241905,340
Honduras,HND,2002,91.46610113,26.83092545,15.199999,-86.241905,340
Honduras,HND,2003,88.96241198,27.42283759,15.199999,-86.241905,340
Honduras,HND,2004,86.80998606,27.05236304,15.199999,-86.241905,340
Honduras,HND,2005,84.50874354,26.78571323,15.199999,-86.241905,340
Honduras,HND,2006,82.63019395,26.88917918,15.199999,-86.241905,340
Honduras,HND,2007,81.01172562,26.7136353,15.199999,-86.241905,340
Honduras,HND,2008,80.48097111,26.87053148,15.199999,-86.241905,340
Honduras,HND,2009,80.98283131,27.30632058,15.199999,-86.241905,340
Honduras,HND,2010,82.36786616,28.64694797,15.199999,-86.241905,340
Honduras,HND,2011,85.65862027,31.5117357,15.199999,-86.241905,340
Honduras,HND,2012,88.41865513,36.07599563,15.199999,-86.241905,340
Honduras,HND,2013,85.94325314,37.17202795,15.199999,-86.241905,340
Honduras,HND,2014,83.12599229,37.71062138,15.199999,-86.241905,340
Honduras,HND,2015,80.60808569,37.1802849,15.199999,-86.241905,340
Honduras,HND,2016,78.22671865,35.10274653,15.199999,-86.241905,340
Honduras,HND,2017,75.81070597,32.82979986,15.199999,-86.241905,340
Honduras,HND,2018,73.0371176,33.27805109,15.199999,-86.241905,340
Honduras,HND,2019,69.95348686,34.31719472,15.199999,-86.241905,340
Hungary,HUN,1990,33.9971071,83.72373719,47.162494,19.503304,348
Hungary,HUN,1991,31.73602093,83.76612695,47.162494,19.503304,348
Hungary,HUN,1992,30.71596528,86.47823015,47.162494,19.503304,348
Hungary,HUN,1993,28.98081812,86.92680141,47.162494,19.503304,348
Hungary,HUN,1994,26.57121685,84.23911592,47.162494,19.503304,348
Hungary,HUN,1995,24.68758834,82.46926313,47.162494,19.503304,348
Hungary,HUN,1996,22.13112971,77.07522775,47.162494,19.503304,348
Hungary,HUN,1997,20.61733999,74.2896596,47.162494,19.503304,348
Hungary,HUN,1998,19.54832361,72.61895513,47.162494,19.503304,348
Hungary,HUN,1999,18.46862045,70.37493739,47.162494,19.503304,348
Hungary,HUN,2000,16.65062836,64.63193518,47.162494,19.503304,348
Hungary,HUN,2001,15.44281027,61.35367878,47.162494,19.503304,348
Hungary,HUN,2002,14.89497472,60.70903599,47.162494,19.503304,348
Hungary,HUN,2003,14.49678679,60.2616273,47.162494,19.503304,348
Hungary,HUN,2004,13.8099407,58.44014904,47.162494,19.503304,348
Hungary,HUN,2005,13.50674488,58.20656739,47.162494,19.503304,348
Hungary,HUN,2006,12.59379844,56.00415454,47.162494,19.503304,348
Hungary,HUN,2007,12.20005375,55.78744992,47.162494,19.503304,348
Hungary,HUN,2008,11.35468659,53.63637925,47.162494,19.503304,348
Hungary,HUN,2009,10.99456894,53.05299119,47.162494,19.503304,348
Hungary,HUN,2010,10.46443921,51.45962196,47.162494,19.503304,348
Hungary,HUN,2011,10.02864226,49.61215921,47.162494,19.503304,348
Hungary,HUN,2012,9.659888636,47.94946381,47.162494,19.503304,348
Hungary,HUN,2013,9.135249065,44.89055051,47.162494,19.503304,348
Hungary,HUN,2014,8.84657336,43.10503287,47.162494,19.503304,348
Hungary,HUN,2015,8.749489239,42.1919839,47.162494,19.503304,348
Hungary,HUN,2016,8.01651162,39.14739266,47.162494,19.503304,348
Hungary,HUN,2017,7.704253253,38.51039939,47.162494,19.503304,348
Hungary,HUN,2018,7.379705813,38.58677388,47.162494,19.503304,348
Hungary,HUN,2019,6.810124856,37.20798918,47.162494,19.503304,348
Iceland,ISL,1990,0.210470803,10.83385765,64.963051,-19.020835,352
Iceland,ISL,1991,0.190580525,10.41583741,64.963051,-19.020835,352
Iceland,ISL,1992,0.17185094,10.08937333,64.963051,-19.020835,352
Iceland,ISL,1993,0.154254811,9.63556642,64.963051,-19.020835,352
Iceland,ISL,1994,0.140334977,9.362310709,64.963051,-19.020835,352
Iceland,ISL,1995,0.129065073,9.201319083,64.963051,-19.020835,352
Iceland,ISL,1996,0.118288788,8.925233429,64.963051,-19.020835,352
Iceland,ISL,1997,0.107858561,8.643389825,64.963051,-19.020835,352
Iceland,ISL,1998,0.098076599,8.323813579,64.963051,-19.020835,352
Iceland,ISL,1999,0.088097537,7.993944551,64.963051,-19.020835,352
Iceland,ISL,2000,0.078124041,7.61823845,64.963051,-19.020835,352
Iceland,ISL,2001,0.070109028,7.40850344,64.963051,-19.020835,352
Iceland,ISL,2002,0.0624965,7.20516427,64.963051,-19.020835,352
Iceland,ISL,2003,0.05471373,6.787946121,64.963051,-19.020835,352
Iceland,ISL,2004,0.048004386,6.347633507,64.963051,-19.020835,352
Iceland,ISL,2005,0.042940603,6.08291495,64.963051,-19.020835,352
Iceland,ISL,2006,0.038898724,5.897339129,64.963051,-19.020835,352
Iceland,ISL,2007,0.035122214,5.801858635,64.963051,-19.020835,352
Iceland,ISL,2008,0.031543049,5.601556396,64.963051,-19.020835,352
Iceland,ISL,2009,0.028524886,5.466124525,64.963051,-19.020835,352
Iceland,ISL,2010,0.025782457,5.276785396,64.963051,-19.020835,352
Iceland,ISL,2011,0.023242357,4.981873654,64.963051,-19.020835,352
Iceland,ISL,2012,0.021032895,4.691456036,64.963051,-19.020835,352
Iceland,ISL,2013,0.018765026,4.250632109,64.963051,-19.020835,352
Iceland,ISL,2014,0.016439447,3.73635114,64.963051,-19.020835,352
Iceland,ISL,2015,0.015130186,3.431560566,64.963051,-19.020835,352
Iceland,ISL,2016,0.014005014,3.241885869,64.963051,-19.020835,352
Iceland,ISL,2017,0.013187834,3.077628576,64.963051,-19.020835,352
Iceland,ISL,2018,0.01241435,3.191583553,64.963051,-19.020835,352
Iceland,ISL,2019,0.011717204,3.133519211,64.963051,-19.020835,352
India,IND,1990,215.5377406,75.60000468,20.593684,78.96288,356
India,IND,1991,213.5701252,75.82280638,20.593684,78.96288,356
India,IND,1992,209.5420945,75.3221707,20.593684,78.96288,356
India,IND,1993,204.1642687,75.10978604,20.593684,78.96288,356
India,IND,1994,197.3794324,74.41076808,20.593684,78.96288,356
India,IND,1995,190.2248754,73.99906344,20.593684,78.96288,356
India,IND,1996,188.1285185,75.53487528,20.593684,78.96288,356
India,IND,1997,191.298379,80.69836536,20.593684,78.96288,356
India,IND,1998,186.4559692,83.27889005,20.593684,78.96288,356
India,IND,1999,175.2604691,83.97152273,20.593684,78.96288,356
India,IND,2000,169.4078886,85.23818593,20.593684,78.96288,356
India,IND,2001,166.2152721,87.61113854,20.593684,78.96288,356
India,IND,2002,160.8684088,87.97256624,20.593684,78.96288,356
India,IND,2003,151.2881283,87.6665501,20.593684,78.96288,356
India,IND,2004,138.0600409,84.29321729,20.593684,78.96288,356
India,IND,2005,134.8785024,87.08127813,20.593684,78.96288,356
India,IND,2006,133.0960578,91.28351857,20.593684,78.96288,356
India,IND,2007,129.2100716,95.27387824,20.593684,78.96288,356
India,IND,2008,124.8393498,98.21752901,20.593684,78.96288,356
India,IND,2009,113.0438264,94.16035493,20.593684,78.96288,356
India,IND,2010,103.5979818,92.43510547,20.593684,78.96288,356
India,IND,2011,97.37418871,96.19762056,20.593684,78.96288,356
India,IND,2012,91.63631956,101.4043958,20.593684,78.96288,356
India,IND,2013,87.55564097,110.4644337,20.593684,78.96288,356
India,IND,2014,81.46432771,114.5453288,20.593684,78.96288,356
India,IND,2015,75.56386336,113.8004838,20.593684,78.96288,356
India,IND,2016,70.48563921,110.9252362,20.593684,78.96288,356
India,IND,2017,66.91832125,109.5118689,20.593684,78.96288,356
India,IND,2018,64.1847226,112.3511504,20.593684,78.96288,356
India,IND,2019,59.58832248,113.9444699,20.593684,78.96288,356
Indonesia,IDN,1990,125.7155792,37.87419228,-0.789275,113.921327,360
Indonesia,IDN,1991,120.0295985,39.5787967,-0.789275,113.921327,360
Indonesia,IDN,1992,114.8135267,41.16913484,-0.789275,113.921327,360
Indonesia,IDN,1993,110.0983251,42.92304588,-0.789275,113.921327,360
Indonesia,IDN,1994,105.5670702,43.95372501,-0.789275,113.921327,360
Indonesia,IDN,1995,101.511469,44.72473697,-0.789275,113.921327,360
Indonesia,IDN,1996,97.70181198,45.61902893,-0.789275,113.921327,360
Indonesia,IDN,1997,94.23311975,46.65972942,-0.789275,113.921327,360
Indonesia,IDN,1998,91.13286624,47.4980488,-0.789275,113.921327,360
Indonesia,IDN,1999,88.34561106,47.75737935,-0.789275,113.921327,360
Indonesia,IDN,2000,86.20891356,48.19462938,-0.789275,113.921327,360
Indonesia,IDN,2001,84.47926452,48.47938113,-0.789275,113.921327,360
Indonesia,IDN,2002,83.07826761,48.73867202,-0.789275,113.921327,360
Indonesia,IDN,2003,81.85567962,49.28587973,-0.789275,113.921327,360
Indonesia,IDN,2004,80.75372662,49.82214163,-0.789275,113.921327,360
Indonesia,IDN,2005,79.62626545,51.20952858,-0.789275,113.921327,360
Indonesia,IDN,2006,78.03349591,52.60395685,-0.789275,113.921327,360
Indonesia,IDN,2007,76.26770343,54.50663426,-0.789275,113.921327,360
Indonesia,IDN,2008,74.47205569,56.21445246,-0.789275,113.921327,360
Indonesia,IDN,2009,72.32606738,57.36938015,-0.789275,113.921327,360
Indonesia,IDN,2010,69.8232099,58.28117419,-0.789275,113.921327,360
Indonesia,IDN,2011,67.21653726,58.62408708,-0.789275,113.921327,360
Indonesia,IDN,2012,64.62337099,58.84125784,-0.789275,113.921327,360
Indonesia,IDN,2013,61.63408744,58.8238766,-0.789275,113.921327,360
Indonesia,IDN,2014,58.46234394,58.29684133,-0.789275,113.921327,360
Indonesia,IDN,2015,55.46724458,57.83024929,-0.789275,113.921327,360
Indonesia,IDN,2016,51.87816479,56.02426918,-0.789275,113.921327,360
Indonesia,IDN,2017,48.33376057,54.42523896,-0.789275,113.921327,360
Indonesia,IDN,2018,44.69732112,56.16503907,-0.789275,113.921327,360
Indonesia,IDN,2019,40.95207617,58.16524903,-0.789275,113.921327,360
Iran,IRN,1990,20.23903223,96.94275994,32.427908,53.688046,364
Iran,IRN,1991,18.0257806,97.4442208,32.427908,53.688046,364
Iran,IRN,1992,15.99286758,98.00714071,32.427908,53.688046,364
Iran,IRN,1993,14.02996495,98.18141645,32.427908,53.688046,364
Iran,IRN,1994,12.28390974,98.40155541,32.427908,53.688046,364
Iran,IRN,1995,10.74089193,98.50102687,32.427908,53.688046,364
Iran,IRN,1996,9.332262253,98.60934841,32.427908,53.688046,364
Iran,IRN,1997,8.017598383,99.15231849,32.427908,53.688046,364
Iran,IRN,1998,6.789694262,99.42789999,32.427908,53.688046,364
Iran,IRN,1999,5.695360738,99.55428376,32.427908,53.688046,364
Iran,IRN,2000,4.801774555,99.0474258,32.427908,53.688046,364
Iran,IRN,2001,3.96832343,97.75845271,32.427908,53.688046,364
Iran,IRN,2002,3.123396239,95.5398468,32.427908,53.688046,364
Iran,IRN,2003,2.371299945,93.03060364,32.427908,53.688046,364
Iran,IRN,2004,1.763524779,89.95436733,32.427908,53.688046,364
Iran,IRN,2005,1.374893321,87.15279326,32.427908,53.688046,364
Iran,IRN,2006,1.138220321,84.86714306,32.427908,53.688046,364
Iran,IRN,2007,0.945848179,82.6628855,32.427908,53.688046,364
Iran,IRN,2008,0.794635681,80.47479467,32.427908,53.688046,364
Iran,IRN,2009,0.677543319,78.67464245,32.427908,53.688046,364
Iran,IRN,2010,0.574477818,76.35191855,32.427908,53.688046,364
Iran,IRN,2011,0.487254018,73.54177893,32.427908,53.688046,364
Iran,IRN,2012,0.418782742,71.98884169,32.427908,53.688046,364
Iran,IRN,2013,0.364576211,71.78111188,32.427908,53.688046,364
Iran,IRN,2014,0.315628758,71.38564491,32.427908,53.688046,364
Iran,IRN,2015,0.274229225,71.81033053,32.427908,53.688046,364
Iran,IRN,2016,0.2330708,70.46056995,32.427908,53.688046,364
Iran,IRN,2017,0.199579571,68.80748265,32.427908,53.688046,364
Iran,IRN,2018,0.169203852,66.93884967,32.427908,53.688046,364
Iran,IRN,2019,0.144527588,66.02609837,32.427908,53.688046,364
Iraq,IRQ,1990,49.60478483,123.9045054,33.223191,43.679291,368
Iraq,IRQ,1991,46.57378688,123.6023046,33.223191,43.679291,368
Iraq,IRQ,1992,44.33642337,125.7244065,33.223191,43.679291,368
Iraq,IRQ,1993,41.89607776,127.9937248,33.223191,43.679291,368
Iraq,IRQ,1994,38.52882046,127.9083653,33.223191,43.679291,368
Iraq,IRQ,1995,35.8255412,130.1871253,33.223191,43.679291,368
Iraq,IRQ,1996,32.75347304,132.65495,33.223191,43.679291,368
Iraq,IRQ,1997,29.278891,135.5777105,33.223191,43.679291,368
Iraq,IRQ,1998,25.58328441,137.5075126,33.223191,43.679291,368
Iraq,IRQ,1999,22.126712,138.6054332,33.223191,43.679291,368
Iraq,IRQ,2000,19.22106456,138.6513611,33.223191,43.679291,368
Iraq,IRQ,2001,16.816546,137.5559383,33.223191,43.679291,368
Iraq,IRQ,2002,14.76994611,136.7844422,33.223191,43.679291,368
Iraq,IRQ,2003,13.06194789,137.4339352,33.223191,43.679291,368
Iraq,IRQ,2004,11.32050075,136.4035245,33.223191,43.679291,368
Iraq,IRQ,2005,9.689464357,135.9499957,33.223191,43.679291,368
Iraq,IRQ,2006,8.033971482,136.3705969,33.223191,43.679291,368
Iraq,IRQ,2007,6.513034142,140.4010475,33.223191,43.679291,368
Iraq,IRQ,2008,5.054233549,143.7887801,33.223191,43.679291,368
Iraq,IRQ,2009,3.779629443,144.6343201,33.223191,43.679291,368
Iraq,IRQ,2010,2.861451071,143.0186047,33.223191,43.679291,368
Iraq,IRQ,2011,2.214947542,140.0778706,33.223191,43.679291,368
Iraq,IRQ,2012,1.667360813,136.7813752,33.223191,43.679291,368
Iraq,IRQ,2013,1.224551469,133.2472545,33.223191,43.679291,368
Iraq,IRQ,2014,0.893135038,130.2446776,33.223191,43.679291,368
Iraq,IRQ,2015,0.671135043,128.1356113,33.223191,43.679291,368
Iraq,IRQ,2016,0.530508889,124.8041767,33.223191,43.679291,368
Iraq,IRQ,2017,0.432147351,121.5741504,33.223191,43.679291,368
Iraq,IRQ,2018,0.359005026,121.6804555,33.223191,43.679291,368
Iraq,IRQ,2019,0.305276543,123.1211507,33.223191,43.679291,368
Ireland,IRL,1990,0.609549103,38.29719485,53.41291,-8.24389,372
Ireland,IRL,1991,0.549656479,36.74446856,53.41291,-8.24389,372
Ireland,IRL,1992,0.499615541,35.33730709,53.41291,-8.24389,372
Ireland,IRL,1993,0.459097756,34.61845157,53.41291,-8.24389,372
Ireland,IRL,1994,0.413703757,33.20823253,53.41291,-8.24389,372
Ireland,IRL,1995,0.381218195,32.55261605,53.41291,-8.24389,372
Ireland,IRL,1996,0.342359819,30.94332309,53.41291,-8.24389,372
Ireland,IRL,1997,0.308335733,29.31747439,53.41291,-8.24389,372
Ireland,IRL,1998,0.277789249,28.28589379,53.41291,-8.24389,372
Ireland,IRL,1999,0.252244023,27.34384608,53.41291,-8.24389,372
Ireland,IRL,2000,0.220017737,25.48235856,53.41291,-8.24389,372
Ireland,IRL,2001,0.187519612,23.26785592,53.41291,-8.24389,372
Ireland,IRL,2002,0.161597422,21.77479729,53.41291,-8.24389,372
Ireland,IRL,2003,0.13867432,20.25107514,53.41291,-8.24389,372
Ireland,IRL,2004,0.119348489,18.8696607,53.41291,-8.24389,372
Ireland,IRL,2005,0.102548388,17.43690661,53.41291,-8.24389,372
Ireland,IRL,2006,0.090804026,16.49952789,53.41291,-8.24389,372
Ireland,IRL,2007,0.079543899,15.60329775,53.41291,-8.24389,372
Ireland,IRL,2008,0.070751929,14.71082798,53.41291,-8.24389,372
Ireland,IRL,2009,0.063363479,14.03851715,53.41291,-8.24389,372
Ireland,IRL,2010,0.054783616,12.64386418,53.41291,-8.24389,372
Ireland,IRL,2011,0.05089545,12.25385365,53.41291,-8.24389,372
Ireland,IRL,2012,0.046756599,11.51934844,53.41291,-8.24389,372
Ireland,IRL,2013,0.042888025,10.64547684,53.41291,-8.24389,372
Ireland,IRL,2014,0.038871373,9.383676801,53.41291,-8.24389,372
Ireland,IRL,2015,0.035503624,8.564350074,53.41291,-8.24389,372
Ireland,IRL,2016,0.031425673,7.569021762,53.41291,-8.24389,372
Ireland,IRL,2017,0.028431285,7.060727934,53.41291,-8.24389,372
Ireland,IRL,2018,0.026693386,7.004711508,53.41291,-8.24389,372
Ireland,IRL,2019,0.025569241,7.223298638,53.41291,-8.24389,372
Israel,ISR,1990,0.322805425,49.33607702,31.046051,34.851612,376
Israel,ISR,1991,0.305697778,51.35779454,31.046051,34.851612,376
Israel,ISR,1992,0.287870899,52.80713911,31.046051,34.851612,376
Israel,ISR,1993,0.25760421,51.41175328,31.046051,34.851612,376
Israel,ISR,1994,0.234163217,50.18757467,31.046051,34.851612,376
Israel,ISR,1995,0.215593415,49.07792204,31.046051,34.851612,376
Israel,ISR,1996,0.196613069,46.87076368,31.046051,34.851612,376
Israel,ISR,1997,0.180753094,45.02381853,31.046051,34.851612,376
Israel,ISR,1998,0.16763521,43.47337944,31.046051,34.851612,376
Israel,ISR,1999,0.152563094,41.34575296,31.046051,34.851612,376
Israel,ISR,2000,0.138196501,39.36321908,31.046051,34.851612,376
Israel,ISR,2001,0.123589831,37.54383256,31.046051,34.851612,376
Israel,ISR,2002,0.111926486,36.41342166,31.046051,34.851612,376
Israel,ISR,2003,0.100927039,35.38527559,31.046051,34.851612,376
Israel,ISR,2004,0.089454186,33.6177049,31.046051,34.851612,376
Israel,ISR,2005,0.080881076,32.45187538,31.046051,34.851612,376
Israel,ISR,2006,0.072534154,31.31764719,31.046051,34.851612,376
Israel,ISR,2007,0.066092482,31.01778058,31.046051,34.851612,376
Israel,ISR,2008,0.058514638,29.81229978,31.046051,34.851612,376
Israel,ISR,2009,0.052312989,28.58832247,31.046051,34.851612,376
Israel,ISR,2010,0.047985964,27.67065712,31.046051,34.851612,376
Israel,ISR,2011,0.045783441,27.22863134,31.046051,34.851612,376
Israel,ISR,2012,0.043084951,26.1267067,31.046051,34.851612,376
Israel,ISR,2013,0.040867311,24.98840233,31.046051,34.851612,376
Israel,ISR,2014,0.038719045,23.74252839,31.046051,34.851612,376
Israel,ISR,2015,0.037279873,23.03220532,31.046051,34.851612,376
Israel,ISR,2016,0.035036144,21.35773552,31.046051,34.851612,376
Israel,ISR,2017,0.033554295,20.40701127,31.046051,34.851612,376
Israel,ISR,2018,0.032500636,20.30814137,31.046051,34.851612,376
Israel,ISR,2019,0.031039695,20.1604603,31.046051,34.851612,376
Italy,ITA,1990,0.951422481,48.60739828,41.87194,12.56738,380
Italy,ITA,1991,0.854503438,47.08806685,41.87194,12.56738,380
Italy,ITA,1992,0.756643522,44.8412507,41.87194,12.56738,380
Italy,ITA,1993,0.670625714,43.28052425,41.87194,12.56738,380
Italy,ITA,1994,0.602245,42.01602552,41.87194,12.56738,380
Italy,ITA,1995,0.538145807,40.53760694,41.87194,12.56738,380
Italy,ITA,1996,0.486515646,39.07326698,41.87194,12.56738,380
Italy,ITA,1997,0.444830063,38.31982539,41.87194,12.56738,380
Italy,ITA,1998,0.412160242,37.89503965,41.87194,12.56738,380
Italy,ITA,1999,0.373285132,36.49800769,41.87194,12.56738,380
Italy,ITA,2000,0.335591184,34.47411488,41.87194,12.56738,380
Italy,ITA,2001,0.300951621,32.7356677,41.87194,12.56738,380
Italy,ITA,2002,0.274687449,31.68977898,41.87194,12.56738,380
Italy,ITA,2003,0.253325264,30.87150259,41.87194,12.56738,380
Italy,ITA,2004,0.221995662,28.58407456,41.87194,12.56738,380
Italy,ITA,2005,0.202362739,27.37675387,41.87194,12.56738,380
Italy,ITA,2006,0.182361919,26.21185901,41.87194,12.56738,380
Italy,ITA,2007,0.166269662,25.25223741,41.87194,12.56738,380
Italy,ITA,2008,0.151891059,24.4522256,41.87194,12.56738,380
Italy,ITA,2009,0.139287158,23.66958178,41.87194,12.56738,380
Italy,ITA,2010,0.126594728,22.70457798,41.87194,12.56738,380
Italy,ITA,2011,0.119029298,22.08571719,41.87194,12.56738,380
Italy,ITA,2012,0.111611349,21.43810182,41.87194,12.56738,380
Italy,ITA,2013,0.103730357,20.37702564,41.87194,12.56738,380
Italy,ITA,2014,0.096886355,19.44438806,41.87194,12.56738,380
Italy,ITA,2015,0.093687074,19.06771088,41.87194,12.56738,380
Italy,ITA,2016,0.085005649,17.28569465,41.87194,12.56738,380
Italy,ITA,2017,0.079743906,16.33219506,41.87194,12.56738,380
Italy,ITA,2018,0.07613385,16.55316531,41.87194,12.56738,380
Italy,ITA,2019,0.072064542,16.62465381,41.87194,12.56738,380
Jamaica,JAM,1990,53.6536086,20.934184,18.109581,-77.297508,388
Jamaica,JAM,1991,45.28166291,19.51385707,18.109581,-77.297508,388
Jamaica,JAM,1992,42.88595513,20.77713482,18.109581,-77.297508,388
Jamaica,JAM,1993,41.02078586,22.50343092,18.109581,-77.297508,388
Jamaica,JAM,1994,37.95620862,23.79635014,18.109581,-77.297508,388
Jamaica,JAM,1995,34.22185714,24.83287532,18.109581,-77.297508,388
Jamaica,JAM,1996,29.97322166,25.46813979,18.109581,-77.297508,388
Jamaica,JAM,1997,26.35233749,26.90758325,18.109581,-77.297508,388
Jamaica,JAM,1998,22.50758751,28.03485927,18.109581,-77.297508,388
Jamaica,JAM,1999,19.93412522,30.02018408,18.109581,-77.297508,388
Jamaica,JAM,2000,17.76539201,30.47600785,18.109581,-77.297508,388
Jamaica,JAM,2001,16.20899152,31.5380013,18.109581,-77.297508,388
Jamaica,JAM,2002,13.88788718,30.3396154,18.109581,-77.297508,388
Jamaica,JAM,2003,12.16599253,29.68012729,18.109581,-77.297508,388
Jamaica,JAM,2004,10.97816722,28.42109061,18.109581,-77.297508,388
Jamaica,JAM,2005,9.980098797,26.62289593,18.109581,-77.297508,388
Jamaica,JAM,2006,9.749951179,26.46269921,18.109581,-77.297508,388
Jamaica,JAM,2007,10.55469467,29.21118545,18.109581,-77.297508,388
Jamaica,JAM,2008,11.25626384,31.59601861,18.109581,-77.297508,388
Jamaica,JAM,2009,11.62035715,32.67363346,18.109581,-77.297508,388
Jamaica,JAM,2010,10.24159166,28.40435758,18.109581,-77.297508,388
Jamaica,JAM,2011,10.50237356,30.54691161,18.109581,-77.297508,388
Jamaica,JAM,2012,9.359119527,28.25807009,18.109581,-77.297508,388
Jamaica,JAM,2013,8.90362124,28.80599882,18.109581,-77.297508,388
Jamaica,JAM,2014,9.173064048,31.75290519,18.109581,-77.297508,388
Jamaica,JAM,2015,8.780867196,32.3832966,18.109581,-77.297508,388
Jamaica,JAM,2016,8.186385257,31.91387259,18.109581,-77.297508,388
Jamaica,JAM,2017,7.619564379,31.5551347,18.109581,-77.297508,388
Jamaica,JAM,2018,7.06830914,31.57234598,18.109581,-77.297508,388
Jamaica,JAM,2019,6.584106344,31.81908468,18.109581,-77.297508,388
Japan,JPN,1990,0.366400448,19.79410479,36.204824,138.252924,392
Japan,JPN,1991,0.322137362,19.118247,36.204824,138.252924,392
Japan,JPN,1992,0.283124424,18.53127594,36.204824,138.252924,392
Japan,JPN,1993,0.248115702,18.03717245,36.204824,138.252924,392
Japan,JPN,1994,0.215357713,17.25993038,36.204824,138.252924,392
Japan,JPN,1995,0.190957051,16.87819587,36.204824,138.252924,392
Japan,JPN,1996,0.16543016,15.91878112,36.204824,138.252924,392
Japan,JPN,1997,0.145479449,15.29017537,36.204824,138.252924,392
Japan,JPN,1998,0.130884918,15.09079664,36.204824,138.252924,392
Japan,JPN,1999,0.117810897,14.88801992,36.204824,138.252924,392
Japan,JPN,2000,0.102633532,14.18743583,36.204824,138.252924,392
Japan,JPN,2001,0.089727102,13.54201327,36.204824,138.252924,392
Japan,JPN,2002,0.078835333,12.93436164,36.204824,138.252924,392
Japan,JPN,2003,0.070069822,12.53728398,36.204824,138.252924,392
Japan,JPN,2004,0.06230325,12.07220382,36.204824,138.252924,392
Japan,JPN,2005,0.056612848,11.82500504,36.204824,138.252924,392
Japan,JPN,2006,0.050738205,11.30711395,36.204824,138.252924,392
Japan,JPN,2007,0.04556599,10.87778733,36.204824,138.252924,392
Japan,JPN,2008,0.041327643,10.51006124,36.204824,138.252924,392
Japan,JPN,2009,0.037789519,10.12751726,36.204824,138.252924,392
Japan,JPN,2010,0.035483257,9.91224084,36.204824,138.252924,392
Japan,JPN,2011,0.033966312,9.959906834,36.204824,138.252924,392
Japan,JPN,2012,0.03219007,10.09461682,36.204824,138.252924,392
Japan,JPN,2013,0.030614002,10.38689179,36.204824,138.252924,392
Japan,JPN,2014,0.029035578,10.53222702,36.204824,138.252924,392
Japan,JPN,2015,0.027381405,10.44927941,36.204824,138.252924,392
Japan,JPN,2016,0.025838591,10.28905621,36.204824,138.252924,392
Japan,JPN,2017,0.024006844,10.01643565,36.204824,138.252924,392
Japan,JPN,2018,0.02281456,9.991029419,36.204824,138.252924,392
Japan,JPN,2019,0.021538113,9.925303333,36.204824,138.252924,392
Jordan,JOR,1990,3.327607599,98.53221552,30.585164,36.238414,400
Jordan,JOR,1991,2.757086441,99.94025907,30.585164,36.238414,400
Jordan,JOR,1992,2.213132806,100.15173,30.585164,36.238414,400
Jordan,JOR,1993,1.835854432,104.2234295,30.585164,36.238414,400
Jordan,JOR,1994,1.472078618,104.8402112,30.585164,36.238414,400
Jordan,JOR,1995,1.219650519,105.6928561,30.585164,36.238414,400
Jordan,JOR,1996,1.030714164,105.3046416,30.585164,36.238414,400
Jordan,JOR,1997,0.849590172,102.5607353,30.585164,36.238414,400
Jordan,JOR,1998,0.702095196,99.75812152,30.585164,36.238414,400
Jordan,JOR,1999,0.582177888,97.12729846,30.585164,36.238414,400
Jordan,JOR,2000,0.4793908,92.91210357,30.585164,36.238414,400
Jordan,JOR,2001,0.412958682,93.16048257,30.585164,36.238414,400
Jordan,JOR,2002,0.349574015,92.71774055,30.585164,36.238414,400
Jordan,JOR,2003,0.284634634,89.40164078,30.585164,36.238414,400
Jordan,JOR,2004,0.246376319,90.43523475,30.585164,36.238414,400
Jordan,JOR,2005,0.215582,91.99624492,30.585164,36.238414,400
Jordan,JOR,2006,0.180509838,89.9111844,30.585164,36.238414,400
Jordan,JOR,2007,0.137426512,81.54536943,30.585164,36.238414,400
Jordan,JOR,2008,0.107685803,75.65273149,30.585164,36.238414,400
Jordan,JOR,2009,0.088782164,72.89503631,30.585164,36.238414,400
Jordan,JOR,2010,0.076004969,71.66598774,30.585164,36.238414,400
Jordan,JOR,2011,0.065765697,70.0212759,30.585164,36.238414,400
Jordan,JOR,2012,0.056183599,67.31523563,30.585164,36.238414,400
Jordan,JOR,2013,0.047816115,64.08740494,30.585164,36.238414,400
Jordan,JOR,2014,0.041966159,62.63667109,30.585164,36.238414,400
Jordan,JOR,2015,0.037432221,61.85403221,30.585164,36.238414,400
Jordan,JOR,2016,0.034535825,60.52014129,30.585164,36.238414,400
Jordan,JOR,2017,0.031977154,58.44373106,30.585164,36.238414,400
Jordan,JOR,2018,0.02956905,57.52226538,30.585164,36.238414,400
Jordan,JOR,2019,0.027134455,56.55773162,30.585164,36.238414,400
Kazakhstan,KAZ,1990,59.6781464,70.23812449,48.019573,66.923684,398
Kazakhstan,KAZ,1991,60.12474191,74.18090925,48.019573,66.923684,398
Kazakhstan,KAZ,1992,61.62374123,79.47853908,48.019573,66.923684,398
Kazakhstan,KAZ,1993,65.18303899,87.66041852,48.019573,66.923684,398
Kazakhstan,KAZ,1994,67.17249804,94.14942408,48.019573,66.923684,398
Kazakhstan,KAZ,1995,67.84645615,99.0989214,48.019573,66.923684,398
Kazakhstan,KAZ,1996,65.55474017,98.71401131,48.019573,66.923684,398
Kazakhstan,KAZ,1997,62.0465665,95.50160266,48.019573,66.923684,398
Kazakhstan,KAZ,1998,58.11902632,91.19984915,48.019573,66.923684,398
Kazakhstan,KAZ,1999,54.54199562,87.65512714,48.019573,66.923684,398
Kazakhstan,KAZ,2000,52.02998881,86.85017182,48.019573,66.923684,398
Kazakhstan,KAZ,2001,49.23839843,85.96621592,48.019573,66.923684,398
Kazakhstan,KAZ,2002,47.0039317,86.48438365,48.019573,66.923684,398
Kazakhstan,KAZ,2003,44.78950479,87.67414018,48.019573,66.923684,398
Kazakhstan,KAZ,2004,41.01575291,85.76193683,48.019573,66.923684,398
Kazakhstan,KAZ,2005,38.07719713,85.38591286,48.019573,66.923684,398
Kazakhstan,KAZ,2006,34.73237913,84.51581411,48.019573,66.923684,398
Kazakhstan,KAZ,2007,31.2835621,84.70318005,48.019573,66.923684,398
Kazakhstan,KAZ,2008,27.20138316,82.46151907,48.019573,66.923684,398
Kazakhstan,KAZ,2009,23.59645333,80.2545079,48.019573,66.923684,398
Kazakhstan,KAZ,2010,21.42321232,80.51080258,48.019573,66.923684,398
Kazakhstan,KAZ,2011,19.55326045,81.05722296,48.019573,66.923684,398
Kazakhstan,KAZ,2012,17.86790519,81.29490257,48.019573,66.923684,398
Kazakhstan,KAZ,2013,16.11029317,79.89590983,48.019573,66.923684,398
Kazakhstan,KAZ,2014,14.58766639,77.9813758,48.019573,66.923684,398
Kazakhstan,KAZ,2015,13.37627884,77.33095644,48.019573,66.923684,398
Kazakhstan,KAZ,2016,12.34001467,76.48177333,48.019573,66.923684,398
Kazakhstan,KAZ,2017,11.33039176,75.41308001,48.019573,66.923684,398
Kazakhstan,KAZ,2018,10.42390363,72.80405771,48.019573,66.923684,398
Kazakhstan,KAZ,2019,9.606289696,71.105531,48.019573,66.923684,398
Kenya,KEN,1990,153.9915459,13.6334216,-0.023559,37.906193,404
Kenya,KEN,1991,151.5423297,14.01278874,-0.023559,37.906193,404
Kenya,KEN,1992,149.4277486,14.45946584,-0.023559,37.906193,404
Kenya,KEN,1993,146.7104273,14.89168676,-0.023559,37.906193,404
Kenya,KEN,1994,143.8696081,15.35762354,-0.023559,37.906193,404
Kenya,KEN,1995,141.2222116,15.87075151,-0.023559,37.906193,404
Kenya,KEN,1996,138.8224925,16.5787336,-0.023559,37.906193,404
Kenya,KEN,1997,137.5720983,17.62392843,-0.023559,37.906193,404
Kenya,KEN,1998,136.6940171,18.73792081,-0.023559,37.906193,404
Kenya,KEN,1999,135.1612976,19.57916463,-0.023559,37.906193,404
Kenya,KEN,2000,135.9716903,20.23375444,-0.023559,37.906193,404
Kenya,KEN,2001,135.5414268,20.49691545,-0.023559,37.906193,404
Kenya,KEN,2002,137.5484917,20.86636109,-0.023559,37.906193,404
Kenya,KEN,2003,138.9713717,21.16690761,-0.023559,37.906193,404
Kenya,KEN,2004,139.9864666,21.4792524,-0.023559,37.906193,404
Kenya,KEN,2005,139.8197346,21.80013089,-0.023559,37.906193,404
Kenya,KEN,2006,138.4021109,22.65795671,-0.023559,37.906193,404
Kenya,KEN,2007,135.8964533,23.7245047,-0.023559,37.906193,404
Kenya,KEN,2008,132.5151749,24.88948756,-0.023559,37.906193,404
Kenya,KEN,2009,129.3092061,26.21656906,-0.023559,37.906193,404
Kenya,KEN,2010,126.2660523,27.40582136,-0.023559,37.906193,404
Kenya,KEN,2011,122.9308857,28.61258848,-0.023559,37.906193,404
Kenya,KEN,2012,118.9512272,29.73076263,-0.023559,37.906193,404
Kenya,KEN,2013,114.5356782,30.86066689,-0.023559,37.906193,404
Kenya,KEN,2014,110.4814562,31.48230388,-0.023559,37.906193,404
Kenya,KEN,2015,106.9811209,31.688354,-0.023559,37.906193,404
Kenya,KEN,2016,103.8530753,30.50536089,-0.023559,37.906193,404
Kenya,KEN,2017,101.4610132,29.01128915,-0.023559,37.906193,404
Kenya,KEN,2018,99.64352649,28.29106345,-0.023559,37.906193,404
Kenya,KEN,2019,97.86995368,26.8420962,-0.023559,37.906193,404
Kiribati,KIR,1990,302.1935386,21.76353849,-3.370417,-168.734039,296
Kiribati,KIR,1991,301.1035712,23.04798662,-3.370417,-168.734039,296
Kiribati,KIR,1992,299.7984949,24.15252517,-3.370417,-168.734039,296
Kiribati,KIR,1993,298.364034,25.26546911,-3.370417,-168.734039,296
Kiribati,KIR,1994,293.0250937,25.65882909,-3.370417,-168.734039,296
Kiribati,KIR,1995,288.5556637,26.04382836,-3.370417,-168.734039,296
Kiribati,KIR,1996,286.1338656,26.6132705,-3.370417,-168.734039,296
Kiribati,KIR,1997,284.8246429,27.2265095,-3.370417,-168.734039,296
Kiribati,KIR,1998,282.5340893,27.52348778,-3.370417,-168.734039,296
Kiribati,KIR,1999,281.1733234,27.65125215,-3.370417,-168.734039,296
Kiribati,KIR,2000,277.6113311,27.34642081,-3.370417,-168.734039,296
Kiribati,KIR,2001,273.054322,27.27677648,-3.370417,-168.734039,296
Kiribati,KIR,2002,268.346442,27.04059918,-3.370417,-168.734039,296
Kiribati,KIR,2003,264.0313978,27.15131728,-3.370417,-168.734039,296
Kiribati,KIR,2004,259.5343719,27.14962336,-3.370417,-168.734039,296
Kiribati,KIR,2005,255.1466242,27.5037571,-3.370417,-168.734039,296
Kiribati,KIR,2006,252.0581125,27.68436026,-3.370417,-168.734039,296
Kiribati,KIR,2007,249.7288699,27.06657715,-3.370417,-168.734039,296
Kiribati,KIR,2008,248.0931018,26.06715708,-3.370417,-168.734039,296
Kiribati,KIR,2009,245.2997235,25.16237266,-3.370417,-168.734039,296
Kiribati,KIR,2010,241.8487939,24.94079162,-3.370417,-168.734039,296
Kiribati,KIR,2011,238.0481507,25.02380685,-3.370417,-168.734039,296
Kiribati,KIR,2012,233.7942781,24.9875035,-3.370417,-168.734039,296
Kiribati,KIR,2013,228.8336101,25.07007129,-3.370417,-168.734039,296
Kiribati,KIR,2014,223.4151993,24.91915089,-3.370417,-168.734039,296
Kiribati,KIR,2015,218.2138159,24.80407186,-3.370417,-168.734039,296
Kiribati,KIR,2016,212.0060712,25.63299608,-3.370417,-168.734039,296
Kiribati,KIR,2017,204.9801585,27.06739533,-3.370417,-168.734039,296
Kiribati,KIR,2018,199.2858291,28.98689833,-3.370417,-168.734039,296
Kiribati,KIR,2019,193.456736,29.71309601,-3.370417,-168.734039,296
Kuwait,KWT,1990,1.434368781,91.99723508,29.31166,47.481766,414
Kuwait,KWT,1991,1.162867813,77.29011018,29.31166,47.481766,414
Kuwait,KWT,1992,0.992970753,69.44463334,29.31166,47.481766,414
Kuwait,KWT,1993,0.917386587,69.48782163,29.31166,47.481766,414
Kuwait,KWT,1994,0.897648961,73.78986382,29.31166,47.481766,414
Kuwait,KWT,1995,0.858077595,77.90380436,29.31166,47.481766,414
Kuwait,KWT,1996,0.721763326,75.10040394,29.31166,47.481766,414
Kuwait,KWT,1997,0.64868125,83.25592446,29.31166,47.481766,414
Kuwait,KWT,1998,0.481601317,79.31506438,29.31166,47.481766,414
Kuwait,KWT,1999,0.394067298,86.56945179,29.31166,47.481766,414
Kuwait,KWT,2000,0.307795305,84.47130078,29.31166,47.481766,414
Kuwait,KWT,2001,0.241368438,76.06519626,29.31166,47.481766,414
Kuwait,KWT,2002,0.223155864,81.22943337,29.31166,47.481766,414
Kuwait,KWT,2003,0.191803684,79.86626558,29.31166,47.481766,414
Kuwait,KWT,2004,0.17227798,81.75877143,29.31166,47.481766,414
Kuwait,KWT,2005,0.155033579,84.09751316,29.31166,47.481766,414
Kuwait,KWT,2006,0.135955936,84.82814607,29.31166,47.481766,414
Kuwait,KWT,2007,0.116781282,83.92199835,29.31166,47.481766,414
Kuwait,KWT,2008,0.11014728,92.08457267,29.31166,47.481766,414
Kuwait,KWT,2009,0.090242251,86.66437942,29.31166,47.481766,414
Kuwait,KWT,2010,0.070284411,76.4549304,29.31166,47.481766,414
Kuwait,KWT,2011,0.057845945,70.88092158,29.31166,47.481766,414
Kuwait,KWT,2012,0.051319879,71.23439005,29.31166,47.481766,414
Kuwait,KWT,2013,0.044129015,68.81705865,29.31166,47.481766,414
Kuwait,KWT,2014,0.038725853,66.93351091,29.31166,47.481766,414
Kuwait,KWT,2015,0.0347634,66.86480293,29.31166,47.481766,414
Kuwait,KWT,2016,0.031586789,66.39684164,29.31166,47.481766,414
Kuwait,KWT,2017,0.029068636,65.9750822,29.31166,47.481766,414
Kuwait,KWT,2018,0.026422962,65.18446977,29.31166,47.481766,414
Kuwait,KWT,2019,0.024329547,65.4549281,29.31166,47.481766,414
Kyrgyzstan,KGZ,1990,114.758505,65.32613104,41.20438,74.766098,417
Kyrgyzstan,KGZ,1991,112.6910446,66.43883873,41.20438,74.766098,417
Kyrgyzstan,KGZ,1992,112.073346,68.40113379,41.20438,74.766098,417
Kyrgyzstan,KGZ,1993,116.2318601,73.73875184,41.20438,74.766098,417
Kyrgyzstan,KGZ,1994,120.139133,79.5114656,41.20438,74.766098,417
Kyrgyzstan,KGZ,1995,117.313886,80.68578841,41.20438,74.766098,417
Kyrgyzstan,KGZ,1996,109.9648933,78.16005008,41.20438,74.766098,417
Kyrgyzstan,KGZ,1997,105.6581704,77.80013142,41.20438,74.766098,417
Kyrgyzstan,KGZ,1998,102.8379213,78.09944558,41.20438,74.766098,417
Kyrgyzstan,KGZ,1999,99.3755125,77.53126509,41.20438,74.766098,417
Kyrgyzstan,KGZ,2000,104.6843838,83.64253736,41.20438,74.766098,417
Kyrgyzstan,KGZ,2001,105.6533161,84.61452372,41.20438,74.766098,417
Kyrgyzstan,KGZ,2002,106.2620779,85.92651533,41.20438,74.766098,417
Kyrgyzstan,KGZ,2003,106.3338435,87.37575383,41.20438,74.766098,417
Kyrgyzstan,KGZ,2004,101.9778779,85.12020135,41.20438,74.766098,417
Kyrgyzstan,KGZ,2005,100.1692073,85.34302572,41.20438,74.766098,417
Kyrgyzstan,KGZ,2006,98.63019005,86.59844788,41.20438,74.766098,417
Kyrgyzstan,KGZ,2007,93.02907282,87.30850044,41.20438,74.766098,417
Kyrgyzstan,KGZ,2008,86.08895887,85.44572641,41.20438,74.766098,417
Kyrgyzstan,KGZ,2009,77.6202386,80.97248909,41.20438,74.766098,417
Kyrgyzstan,KGZ,2010,71.06957623,77.61060608,41.20438,74.766098,417
Kyrgyzstan,KGZ,2011,65.54181304,75.91781443,41.20438,74.766098,417
Kyrgyzstan,KGZ,2012,60.00149428,75.34563053,41.20438,74.766098,417
Kyrgyzstan,KGZ,2013,54.36800963,73.80452289,41.20438,74.766098,417
Kyrgyzstan,KGZ,2014,50.37456633,73.2730259,41.20438,74.766098,417
Kyrgyzstan,KGZ,2015,47.92286985,74.37769576,41.20438,74.766098,417
Kyrgyzstan,KGZ,2016,43.17915963,70.78279529,41.20438,74.766098,417
Kyrgyzstan,KGZ,2017,40.33882345,70.00436158,41.20438,74.766098,417
Kyrgyzstan,KGZ,2018,37.21412013,67.4429687,41.20438,74.766098,417
Kyrgyzstan,KGZ,2019,35.10577727,67.85069819,41.20438,74.766098,417
Laos,LAO,1990,325.800439,25.53448126,19.85627,102.495496,418
Laos,LAO,1991,320.647587,26.12071392,19.85627,102.495496,418
Laos,LAO,1992,315.959646,26.66675892,19.85627,102.495496,418
Laos,LAO,1993,311.6735219,27.18598612,19.85627,102.495496,418
Laos,LAO,1994,307.2038443,27.55386342,19.85627,102.495496,418
Laos,LAO,1995,302.546141,28.01990014,19.85627,102.495496,418
Laos,LAO,1996,297.3560213,28.51008042,19.85627,102.495496,418
Laos,LAO,1997,292.4139401,29.41372,19.85627,102.495496,418
Laos,LAO,1998,287.5142758,29.74807427,19.85627,102.495496,418
Laos,LAO,1999,282.3947136,29.48664174,19.85627,102.495496,418
Laos,LAO,2000,276.3921347,28.95723729,19.85627,102.495496,418
Laos,LAO,2001,271.6380516,29.56087986,19.85627,102.495496,418
Laos,LAO,2002,263.8784864,30.41611136,19.85627,102.495496,418
Laos,LAO,2003,256.6569163,32.05184165,19.85627,102.495496,418
Laos,LAO,2004,248.6681458,32.79856473,19.85627,102.495496,418
Laos,LAO,2005,241.0860532,33.12580295,19.85627,102.495496,418
Laos,LAO,2006,233.0339644,33.59537469,19.85627,102.495496,418
Laos,LAO,2007,224.0979858,34.8761874,19.85627,102.495496,418
Laos,LAO,2008,216.8710423,36.24346098,19.85627,102.495496,418
Laos,LAO,2009,208.5037995,36.71524455,19.85627,102.495496,418
Laos,LAO,2010,200.2818909,36.99325022,19.85627,102.495496,418
Laos,LAO,2011,192.6358176,36.73945266,19.85627,102.495496,418
Laos,LAO,2012,186.2562695,36.32971724,19.85627,102.495496,418
Laos,LAO,2013,180.6105467,35.28367352,19.85627,102.495496,418
Laos,LAO,2014,175.4376714,34.11719885,19.85627,102.495496,418
Laos,LAO,2015,171.1215782,33.82761186,19.85627,102.495496,418
Laos,LAO,2016,166.8201942,32.94513854,19.85627,102.495496,418
Laos,LAO,2017,162.9297818,32.80801636,19.85627,102.495496,418
Laos,LAO,2018,159.342708,34.52248289,19.85627,102.495496,418
Laos,LAO,2019,155.4091872,37.16979527,19.85627,102.495496,418
Latvia,LVA,1990,15.72124683,75.87711156,56.879635,24.603189,428
Latvia,LVA,1991,14.48921656,76.15170795,56.879635,24.603189,428
Latvia,LVA,1992,13.67719891,77.98454137,56.879635,24.603189,428
Latvia,LVA,1993,14.07274802,86.78834691,56.879635,24.603189,428
Latvia,LVA,1994,14.20383946,93.11763606,56.879635,24.603189,428
Latvia,LVA,1995,12.77182951,86.51599192,56.879635,24.603189,428
Latvia,LVA,1996,10.76460855,73.56934401,56.879635,24.603189,428
Latvia,LVA,1997,10.08885921,68.47654392,56.879635,24.603189,428
Latvia,LVA,1998,10.15836155,68.44030805,56.879635,24.603189,428
Latvia,LVA,1999,9.376756136,62.8028988,56.879635,24.603189,428
Latvia,LVA,2000,8.795729915,59.85381303,56.879635,24.603189,428
Latvia,LVA,2001,8.855415112,62.07607038,56.879635,24.603189,428
Latvia,LVA,2002,8.300963389,60.5102619,56.879635,24.603189,428
Latvia,LVA,2003,7.795755531,58.9114689,56.879635,24.603189,428
Latvia,LVA,2004,7.22634559,57.38194373,56.879635,24.603189,428
Latvia,LVA,2005,6.971864111,58.69072716,56.879635,24.603189,428
Latvia,LVA,2006,6.800766363,60.9474268,56.879635,24.603189,428
Latvia,LVA,2007,6.116765001,59.68570146,56.879635,24.603189,428
Latvia,LVA,2008,5.213181339,55.28458778,56.879635,24.603189,428
Latvia,LVA,2009,4.603676483,52.55288366,56.879635,24.603189,428
Latvia,LVA,2010,4.230825525,51.17199206,56.879635,24.603189,428
Latvia,LVA,2011,3.907062456,48.22108537,56.879635,24.603189,428
Latvia,LVA,2012,3.66084195,44.8327088,56.879635,24.603189,428
Latvia,LVA,2013,3.55742115,41.99513788,56.879635,24.603189,428
Latvia,LVA,2014,3.299429216,37.35630303,56.879635,24.603189,428
Latvia,LVA,2015,3.078029093,33.49664331,56.879635,24.603189,428
Latvia,LVA,2016,2.831336494,28.83314266,56.879635,24.603189,428
Latvia,LVA,2017,2.660194989,26.410471,56.879635,24.603189,428
Latvia,LVA,2018,2.530223474,26.37204197,56.879635,24.603189,428
Latvia,LVA,2019,2.418707589,26.67624267,56.879635,24.603189,428
Lebanon,LBN,1990,19.02123794,77.14214529,33.854721,35.862285,422
Lebanon,LBN,1991,16.44987455,78.49132954,33.854721,35.862285,422
Lebanon,LBN,1992,14.2489229,80.09695914,33.854721,35.862285,422
Lebanon,LBN,1993,12.2771009,81.1818386,33.854721,35.862285,422
Lebanon,LBN,1994,10.42952344,80.41725454,33.854721,35.862285,422
Lebanon,LBN,1995,8.901331872,78.86048136,33.854721,35.862285,422
Lebanon,LBN,1996,7.636580288,76.97279314,33.854721,35.862285,422
Lebanon,LBN,1997,6.562496943,75.40734875,33.854721,35.862285,422
Lebanon,LBN,1998,5.620401332,73.57620094,33.854721,35.862285,422
Lebanon,LBN,1999,4.791022878,71.84471449,33.854721,35.862285,422
Lebanon,LBN,2000,4.104654345,70.4666174,33.854721,35.862285,422
Lebanon,LBN,2001,3.520028996,69.7866672,33.854721,35.862285,422
Lebanon,LBN,2002,3.010879468,69.45705551,33.854721,35.862285,422
Lebanon,LBN,2003,2.576521577,69.86723696,33.854721,35.862285,422
Lebanon,LBN,2004,2.206052718,70.40598237,33.854721,35.862285,422
Lebanon,LBN,2005,1.894611267,71.16056872,33.854721,35.862285,422
Lebanon,LBN,2006,1.621541861,72.42920141,33.854721,35.862285,422
Lebanon,LBN,2007,1.370455708,74.59776005,33.854721,35.862285,422
Lebanon,LBN,2008,1.14536014,76.84385467,33.854721,35.862285,422
Lebanon,LBN,2009,0.949776241,78.10795193,33.854721,35.862285,422
Lebanon,LBN,2010,0.792875139,78.18506285,33.854721,35.862285,422
Lebanon,LBN,2011,0.669370556,78.00250599,33.854721,35.862285,422
Lebanon,LBN,2012,0.556817037,77.38967679,33.854721,35.862285,422
Lebanon,LBN,2013,0.460796576,76.62891042,33.854721,35.862285,422
Lebanon,LBN,2014,0.382715798,75.72426476,33.854721,35.862285,422
Lebanon,LBN,2015,0.32254406,74.56074777,33.854721,35.862285,422
Lebanon,LBN,2016,0.280090455,71.39183904,33.854721,35.862285,422
Lebanon,LBN,2017,0.246216095,68.28885397,33.854721,35.862285,422
Lebanon,LBN,2018,0.214033732,66.83664551,33.854721,35.862285,422
Lebanon,LBN,2019,0.185797233,65.64718614,33.854721,35.862285,422
Lesotho,LSO,1990,180.2664882,31.76673868,-29.609988,28.233608,426
Lesotho,LSO,1991,175.4081218,32.93554329,-29.609988,28.233608,426
Lesotho,LSO,1992,171.6795185,34.15260022,-29.609988,28.233608,426
Lesotho,LSO,1993,167.8347218,35.3243315,-29.609988,28.233608,426
Lesotho,LSO,1994,165.2728862,36.37708495,-29.609988,28.233608,426
Lesotho,LSO,1995,161.7958921,37.20024766,-29.609988,28.233608,426
Lesotho,LSO,1996,157.8440471,37.83350792,-29.609988,28.233608,426
Lesotho,LSO,1997,154.9094574,38.90638942,-29.609988,28.233608,426
Lesotho,LSO,1998,156.9216045,40.92820426,-29.609988,28.233608,426
Lesotho,LSO,1999,159.4523875,42.96451458,-29.609988,28.233608,426
Lesotho,LSO,2000,166.2858849,44.99895832,-29.609988,28.233608,426
Lesotho,LSO,2001,168.6517349,46.1047382,-29.609988,28.233608,426
Lesotho,LSO,2002,173.5923072,47.46128414,-29.609988,28.233608,426
Lesotho,LSO,2003,179.8700432,49.64043538,-29.609988,28.233608,426
Lesotho,LSO,2004,184.3074669,52.45839001,-29.609988,28.233608,426
Lesotho,LSO,2005,186.8465436,55.10080029,-29.609988,28.233608,426
Lesotho,LSO,2006,186.6311503,58.41082502,-29.609988,28.233608,426
Lesotho,LSO,2007,185.4227385,61.31628666,-29.609988,28.233608,426
Lesotho,LSO,2008,184.0829251,64.7840872,-29.609988,28.233608,426
Lesotho,LSO,2009,179.1150111,67.30069745,-29.609988,28.233608,426
Lesotho,LSO,2010,176.2782193,69.72800385,-29.609988,28.233608,426
Lesotho,LSO,2011,172.6692186,72.45162474,-29.609988,28.233608,426
Lesotho,LSO,2012,170.6628892,75.4401005,-29.609988,28.233608,426
Lesotho,LSO,2013,167.8852308,78.58271334,-29.609988,28.233608,426
Lesotho,LSO,2014,164.3269975,78.76948132,-29.609988,28.233608,426
Lesotho,LSO,2015,159.0352324,78.14165838,-29.609988,28.233608,426
Lesotho,LSO,2016,151.2756663,76.2726243,-29.609988,28.233608,426
Lesotho,LSO,2017,143.9852333,74.73951505,-29.609988,28.233608,426
Lesotho,LSO,2018,138.2825522,73.46170908,-29.609988,28.233608,426
Lesotho,LSO,2019,133.4403164,72.44415628,-29.609988,28.233608,426
Liberia,LBR,1990,239.6102368,24.7145556,6.428055,-9.429499,430
Liberia,LBR,1991,231.5583635,21.83434116,6.428055,-9.429499,430
Liberia,LBR,1992,233.7645058,20.22794361,6.428055,-9.429499,430
Liberia,LBR,1993,235.3967957,19.05952846,6.428055,-9.429499,430
Liberia,LBR,1994,233.2635509,18.08327021,6.428055,-9.429499,430
Liberia,LBR,1995,227.1446171,17.33029567,6.428055,-9.429499,430
Liberia,LBR,1996,226.6470449,17.62308919,6.428055,-9.429499,430
Liberia,LBR,1997,220.7596792,17.82637508,6.428055,-9.429499,430
Liberia,LBR,1998,215.4262888,18.37181617,6.428055,-9.429499,430
Liberia,LBR,1999,207.1752546,18.59378983,6.428055,-9.429499,430
Liberia,LBR,2000,202.4992732,18.94742119,6.428055,-9.429499,430
Liberia,LBR,2001,193.9586073,19.2905011,6.428055,-9.429499,430
Liberia,LBR,2002,187.6796058,20.19498583,6.428055,-9.429499,430
Liberia,LBR,2003,179.4843494,21.04270459,6.428055,-9.429499,430
Liberia,LBR,2004,172.8214642,21.74993996,6.428055,-9.429499,430
Liberia,LBR,2005,168.5732155,22.26839349,6.428055,-9.429499,430
Liberia,LBR,2006,167.3258725,22.83374231,6.428055,-9.429499,430
Liberia,LBR,2007,164.6890338,22.9104096,6.428055,-9.429499,430
Liberia,LBR,2008,164.1561956,22.99384192,6.428055,-9.429499,430
Liberia,LBR,2009,163.3901799,23.15547374,6.428055,-9.429499,430
Liberia,LBR,2010,161.5286969,23.54232976,6.428055,-9.429499,430
Liberia,LBR,2011,157.9171168,25.05808874,6.428055,-9.429499,430
Liberia,LBR,2012,154.4637693,28.07639789,6.428055,-9.429499,430
Liberia,LBR,2013,147.9229363,30.88914037,6.428055,-9.429499,430
Liberia,LBR,2014,139.3698009,32.21438056,6.428055,-9.429499,430
Liberia,LBR,2015,135.6362922,32.72993193,6.428055,-9.429499,430
Liberia,LBR,2016,131.5618092,30.52708111,6.428055,-9.429499,430
Liberia,LBR,2017,128.0242897,28.68076856,6.428055,-9.429499,430
Liberia,LBR,2018,125.542763,29.73465411,6.428055,-9.429499,430
Liberia,LBR,2019,122.113078,31.46573001,6.428055,-9.429499,430
Libya,LBY,1990,27.93773435,63.44710889,26.3351,17.228331,434
Libya,LBY,1991,22.79444245,65.88516452,26.3351,17.228331,434
Libya,LBY,1992,17.93312401,66.94591023,26.3351,17.228331,434
Libya,LBY,1993,14.100825,68.40419586,26.3351,17.228331,434
Libya,LBY,1994,10.98610677,69.03636747,26.3351,17.228331,434
Libya,LBY,1995,8.680097363,68.874954,26.3351,17.228331,434
Libya,LBY,1996,6.963294188,68.14054444,26.3351,17.228331,434
Libya,LBY,1997,5.742691037,70.08960359,26.3351,17.228331,434
Libya,LBY,1998,4.767606081,72.86091471,26.3351,17.228331,434
Libya,LBY,1999,3.873779096,74.48415777,26.3351,17.228331,434
Libya,LBY,2000,3.152944026,75.21203785,26.3351,17.228331,434
Libya,LBY,2001,2.574639889,76.37500203,26.3351,17.228331,434
Libya,LBY,2002,2.076542423,77.6327454,26.3351,17.228331,434
Libya,LBY,2003,1.603225512,75.97344564,26.3351,17.228331,434
Libya,LBY,2004,1.201703874,71.64860874,26.3351,17.228331,434
Libya,LBY,2005,0.961177011,70.7277529,26.3351,17.228331,434
Libya,LBY,2006,0.789142439,71.2552423,26.3351,17.228331,434
Libya,LBY,2007,0.701223381,77.8765211,26.3351,17.228331,434
Libya,LBY,2008,0.56984611,78.40297907,26.3351,17.228331,434
Libya,LBY,2009,0.482244251,80.4090873,26.3351,17.228331,434
Libya,LBY,2010,0.396575108,77.63092921,26.3351,17.228331,434
Libya,LBY,2011,0.350602233,76.73456961,26.3351,17.228331,434
Libya,LBY,2012,0.311005907,73.84176152,26.3351,17.228331,434
Libya,LBY,2013,0.284151563,72.23948753,26.3351,17.228331,434
Libya,LBY,2014,0.264380983,71.40700981,26.3351,17.228331,434
Libya,LBY,2015,0.245141233,70.85496972,26.3351,17.228331,434
Libya,LBY,2016,0.228714221,70.54650822,26.3351,17.228331,434
Libya,LBY,2017,0.211030552,70.48439448,26.3351,17.228331,434
Libya,LBY,2018,0.188446874,71.35574113,26.3351,17.228331,434
Libya,LBY,2019,0.162828044,72.26731649,26.3351,17.228331,434
Lithuania,LTU,1990,10.68415144,57.61827383,55.169438,23.881275,440
Lithuania,LTU,1991,10.33383092,59.73570804,55.169438,23.881275,440
Lithuania,LTU,1992,9.469610259,58.37214325,55.169438,23.881275,440
Lithuania,LTU,1993,9.663288417,63.48089218,55.169438,23.881275,440
Lithuania,LTU,1994,9.23955944,63.96666935,55.169438,23.881275,440
Lithuania,LTU,1995,8.424722894,61.19287042,55.169438,23.881275,440
Lithuania,LTU,1996,7.415238343,55.55892481,55.169438,23.881275,440
Lithuania,LTU,1997,6.63278805,50.26623058,55.169438,23.881275,440
Lithuania,LTU,1998,6.231159698,47.71016715,55.169438,23.881275,440
Lithuania,LTU,1999,5.669716606,44.29020674,55.169438,23.881275,440
Lithuania,LTU,2000,5.181517757,42.28785021,55.169438,23.881275,440
Lithuania,LTU,2001,5.005506713,43.54483708,55.169438,23.881275,440
Lithuania,LTU,2002,4.558271217,42.58445242,55.169438,23.881275,440
Lithuania,LTU,2003,4.197161436,42.23573386,55.169438,23.881275,440
Lithuania,LTU,2004,3.822408591,41.62255492,55.169438,23.881275,440
Lithuania,LTU,2005,3.709130342,43.82519236,55.169438,23.881275,440
Lithuania,LTU,2006,3.492783762,44.85082924,55.169438,23.881275,440
Lithuania,LTU,2007,3.24866814,46.07443337,55.169438,23.881275,440
Lithuania,LTU,2008,2.869094659,44.3954616,55.169438,23.881275,440
Lithuania,LTU,2009,2.398931164,40.67828534,55.169438,23.881275,440
Lithuania,LTU,2010,2.206615057,40.53313326,55.169438,23.881275,440
Lithuania,LTU,2011,2.010239954,38.93609521,55.169438,23.881275,440
Lithuania,LTU,2012,1.836033889,36.51133568,55.169438,23.881275,440
Lithuania,LTU,2013,1.715510166,34.34193903,55.169438,23.881275,440
Lithuania,LTU,2014,1.530186728,30.46669875,55.169438,23.881275,440
Lithuania,LTU,2015,1.436705581,28.46375768,55.169438,23.881275,440
Lithuania,LTU,2016,1.301000839,24.87004071,55.169438,23.881275,440
Lithuania,LTU,2017,1.125965652,21.04983002,55.169438,23.881275,440
Lithuania,LTU,2018,1.050530482,20.93374224,55.169438,23.881275,440
Lithuania,LTU,2019,0.98426932,20.87682389,55.169438,23.881275,440
Luxembourg,LUX,1990,0.230731897,40.07416415,49.815273,6.129583,442
Luxembourg,LUX,1991,0.217399345,38.51018483,49.815273,6.129583,442
Luxembourg,LUX,1992,0.202980357,36.56251253,49.815273,6.129583,442
Luxembourg,LUX,1993,0.190754379,35.18519791,49.815273,6.129583,442
Luxembourg,LUX,1994,0.17683098,33.52542642,49.815273,6.129583,442
Luxembourg,LUX,1995,0.165198163,32.03208693,49.815273,6.129583,442
Luxembourg,LUX,1996,0.154665155,30.56373159,49.815273,6.129583,442
Luxembourg,LUX,1997,0.142687281,28.57766562,49.815273,6.129583,442
Luxembourg,LUX,1998,0.131932813,26.97991562,49.815273,6.129583,442
Luxembourg,LUX,1999,0.121303532,25.09861213,49.815273,6.129583,442
Luxembourg,LUX,2000,0.111819688,23.91024725,49.815273,6.129583,442
Luxembourg,LUX,2001,0.101134386,22.30473381,49.815273,6.129583,442
Luxembourg,LUX,2002,0.093111825,22.01059094,49.815273,6.129583,442
Luxembourg,LUX,2003,0.084763023,21.05524308,49.815273,6.129583,442
Luxembourg,LUX,2004,0.077748087,20.4524166,49.815273,6.129583,442
Luxembourg,LUX,2005,0.070747005,19.52021704,49.815273,6.129583,442
Luxembourg,LUX,2006,0.064190647,18.87072251,49.815273,6.129583,442
Luxembourg,LUX,2007,0.057078464,18.19638685,49.815273,6.129583,442
Luxembourg,LUX,2008,0.050732873,17.55489021,49.815273,6.129583,442
Luxembourg,LUX,2009,0.045947146,17.48417632,49.815273,6.129583,442
Luxembourg,LUX,2010,0.041658932,17.12150889,49.815273,6.129583,442
Luxembourg,LUX,2011,0.037774733,16.22432336,49.815273,6.129583,442
Luxembourg,LUX,2012,0.034289213,14.98719155,49.815273,6.129583,442
Luxembourg,LUX,2013,0.031265694,13.5904827,49.815273,6.129583,442
Luxembourg,LUX,2014,0.028122402,12.24393055,49.815273,6.129583,442
Luxembourg,LUX,2015,0.025185591,10.91840812,49.815273,6.129583,442
Luxembourg,LUX,2016,0.022379805,9.766685871,49.815273,6.129583,442
Luxembourg,LUX,2017,0.020992447,9.27266015,49.815273,6.129583,442
Luxembourg,LUX,2018,0.019923843,9.395743137,49.815273,6.129583,442
Luxembourg,LUX,2019,0.019128874,9.618828399,49.815273,6.129583,442
Madagascar,MDG,1990,252.6521977,11.48607481,-18.766947,46.869107,450
Madagascar,MDG,1991,253.0268579,11.50920223,-18.766947,46.869107,450
Madagascar,MDG,1992,252.7927538,11.4983697,-18.766947,46.869107,450
Madagascar,MDG,1993,258.5626084,11.83757345,-18.766947,46.869107,450
Madagascar,MDG,1994,250.8020334,11.53374333,-18.766947,46.869107,450
Madagascar,MDG,1995,264.0629764,12.25822004,-18.766947,46.869107,450
Madagascar,MDG,1996,263.9078054,12.4422396,-18.766947,46.869107,450
Madagascar,MDG,1997,262.7078225,12.68899312,-18.766947,46.869107,450
Madagascar,MDG,1998,262.3617166,13.12431256,-18.766947,46.869107,450
Madagascar,MDG,1999,256.4519889,13.34484251,-18.766947,46.869107,450
Madagascar,MDG,2000,252.0383167,13.5422472,-18.766947,46.869107,450
Madagascar,MDG,2001,245.9228909,13.86954392,-18.766947,46.869107,450
Madagascar,MDG,2002,243.9321194,14.61075594,-18.766947,46.869107,450
Madagascar,MDG,2003,240.4804274,15.41571548,-18.766947,46.869107,450
Madagascar,MDG,2004,235.3262113,16.01307776,-18.766947,46.869107,450
Madagascar,MDG,2005,230.2731313,16.46133474,-18.766947,46.869107,450
Madagascar,MDG,2006,225.6089883,16.87540601,-18.766947,46.869107,450
Madagascar,MDG,2007,221.455696,16.78955716,-18.766947,46.869107,450
Madagascar,MDG,2008,221.3969972,16.78035154,-18.766947,46.869107,450
Madagascar,MDG,2009,220.2407969,16.82058018,-18.766947,46.869107,450
Madagascar,MDG,2010,217.5258226,17.07113972,-18.766947,46.869107,450
Madagascar,MDG,2011,213.9952237,17.80435328,-18.766947,46.869107,450
Madagascar,MDG,2012,208.7625791,18.75748517,-18.766947,46.869107,450
Madagascar,MDG,2013,203.2486418,19.78668915,-18.766947,46.869107,450
Madagascar,MDG,2014,198.2521858,20.22483867,-18.766947,46.869107,450
Madagascar,MDG,2015,194.1931557,20.30956384,-18.766947,46.869107,450
Madagascar,MDG,2016,190.5272228,19.5898452,-18.766947,46.869107,450
Madagascar,MDG,2017,187.4572474,19.06060225,-18.766947,46.869107,450
Madagascar,MDG,2018,184.7967687,20.02571332,-18.766947,46.869107,450
Madagascar,MDG,2019,181.0099385,20.77874131,-18.766947,46.869107,450
Malawi,MWI,1990,236.6930917,10.64602087,-13.254308,34.301525,454
Malawi,MWI,1991,234.8597766,10.66413811,-13.254308,34.301525,454
Malawi,MWI,1992,234.9434402,10.66774447,-13.254308,34.301525,454
Malawi,MWI,1993,235.8622769,10.7397401,-13.254308,34.301525,454
Malawi,MWI,1994,238.4378217,10.88402295,-13.254308,34.301525,454
Malawi,MWI,1995,237.5296605,10.99299138,-13.254308,34.301525,454
Malawi,MWI,1996,235.8038774,11.18845717,-13.254308,34.301525,454
Malawi,MWI,1997,234.2922346,11.6880994,-13.254308,34.301525,454
Malawi,MWI,1998,234.1895724,12.29397423,-13.254308,34.301525,454
Malawi,MWI,1999,232.3795516,12.84226224,-13.254308,34.301525,454
Malawi,MWI,2000,228.1637652,12.92896827,-13.254308,34.301525,454
Malawi,MWI,2001,220.4257171,12.84252274,-13.254308,34.301525,454
Malawi,MWI,2002,215.6143575,12.74554884,-13.254308,34.301525,454
Malawi,MWI,2003,211.0079311,12.72355718,-13.254308,34.301525,454
Malawi,MWI,2004,206.5517583,12.98300098,-13.254308,34.301525,454
Malawi,MWI,2005,199.8130998,13.3819847,-13.254308,34.301525,454
Malawi,MWI,2006,194.3865861,14.39321035,-13.254308,34.301525,454
Malawi,MWI,2007,187.6956791,14.71666108,-13.254308,34.301525,454
Malawi,MWI,2008,182.1524366,14.87428505,-13.254308,34.301525,454
Malawi,MWI,2009,178.3161002,15.10182926,-13.254308,34.301525,454
Malawi,MWI,2010,175.3217809,15.72803754,-13.254308,34.301525,454
Malawi,MWI,2011,170.9260711,16.51899336,-13.254308,34.301525,454
Malawi,MWI,2012,165.7606024,17.29140096,-13.254308,34.301525,454
Malawi,MWI,2013,160.5478978,17.94863761,-13.254308,34.301525,454
Malawi,MWI,2014,155.7445942,18.10007778,-13.254308,34.301525,454
Malawi,MWI,2015,152.3850653,18.06216986,-13.254308,34.301525,454
Malawi,MWI,2016,149.34089,17.51873295,-13.254308,34.301525,454
Malawi,MWI,2017,145.899297,16.93457325,-13.254308,34.301525,454
Malawi,MWI,2018,144.1288682,16.7466767,-13.254308,34.301525,454
Malawi,MWI,2019,141.8994356,16.61100726,-13.254308,34.301525,454
Malaysia,MYS,1990,9.433571578,80.82683826,4.210484,101.975766,458
Malaysia,MYS,1991,8.244050138,75.8982611,4.210484,101.975766,458
Malaysia,MYS,1992,7.306040107,72.8810829,4.210484,101.975766,458
Malaysia,MYS,1993,6.612779426,71.86276024,4.210484,101.975766,458
Malaysia,MYS,1994,6.19513892,74.07203459,4.210484,101.975766,458
Malaysia,MYS,1995,5.710056539,75.77023041,4.210484,101.975766,458
Malaysia,MYS,1996,4.725244154,71.33036139,4.210484,101.975766,458
Malaysia,MYS,1997,3.91634873,67.68688521,4.210484,101.975766,458
Malaysia,MYS,1998,3.240246119,64.26399133,4.210484,101.975766,458
Malaysia,MYS,1999,3.022143762,68.40117635,4.210484,101.975766,458
Malaysia,MYS,2000,2.497035419,63.79468221,4.210484,101.975766,458
Malaysia,MYS,2001,2.221657074,63.09531806,4.210484,101.975766,458
Malaysia,MYS,2002,2.03024651,63.45647578,4.210484,101.975766,458
Malaysia,MYS,2003,1.825737132,63.35739259,4.210484,101.975766,458
Malaysia,MYS,2004,1.606645377,60.92018986,4.210484,101.975766,458
Malaysia,MYS,2005,1.452759079,59.6703217,4.210484,101.975766,458
Malaysia,MYS,2006,1.32471116,57.6771714,4.210484,101.975766,458
Malaysia,MYS,2007,1.216724217,55.34079924,4.210484,101.975766,458
Malaysia,MYS,2008,1.160249889,54.70026419,4.210484,101.975766,458
Malaysia,MYS,2009,1.102579398,53.96040302,4.210484,101.975766,458
Malaysia,MYS,2010,1.002338999,51.99530393,4.210484,101.975766,458
Malaysia,MYS,2011,0.908435934,50.7247324,4.210484,101.975766,458
Malaysia,MYS,2012,0.837595881,50.21854901,4.210484,101.975766,458
Malaysia,MYS,2013,0.74524869,47.89792895,4.210484,101.975766,458
Malaysia,MYS,2014,0.701841332,48.64850859,4.210484,101.975766,458
Malaysia,MYS,2015,0.648462625,48.42020173,4.210484,101.975766,458
Malaysia,MYS,2016,0.600724141,46.14056155,4.210484,101.975766,458
Malaysia,MYS,2017,0.549971273,43.40552749,4.210484,101.975766,458
Malaysia,MYS,2018,0.499956606,43.97872008,4.210484,101.975766,458
Malaysia,MYS,2019,0.462462652,45.23283429,4.210484,101.975766,458
Maldives,MDV,1990,168.0353551,30.36329396,3.202778,73.22068,462
Maldives,MDV,1991,164.6026627,33.04682502,3.202778,73.22068,462
Maldives,MDV,1992,158.9625713,34.87520019,3.202778,73.22068,462
Maldives,MDV,1993,148.5321701,35.45904412,3.202778,73.22068,462
Maldives,MDV,1994,135.061314,34.76356025,3.202778,73.22068,462
Maldives,MDV,1995,127.9403422,35.13331245,3.202778,73.22068,462
Maldives,MDV,1996,122.9518831,35.13076136,3.202778,73.22068,462
Maldives,MDV,1997,114.0705994,33.79139738,3.202778,73.22068,462
Maldives,MDV,1998,99.4937027,30.51559771,3.202778,73.22068,462
Maldives,MDV,1999,88.06888478,28.70582947,3.202778,73.22068,462
Maldives,MDV,2000,80.83161564,27.68099976,3.202778,73.22068,462
Maldives,MDV,2001,73.08144625,27.64896968,3.202778,73.22068,462
Maldives,MDV,2002,61.76231311,26.05617773,3.202778,73.22068,462
Maldives,MDV,2003,53.43518874,26.00018295,3.202778,73.22068,462
Maldives,MDV,2004,45.63324524,25.26929793,3.202778,73.22068,462
Maldives,MDV,2005,39.47816268,24.95410692,3.202778,73.22068,462
Maldives,MDV,2006,34.34211175,24.80917365,3.202778,73.22068,462
Maldives,MDV,2007,29.7815234,25.26799621,3.202778,73.22068,462
Maldives,MDV,2008,25.99854984,25.30938734,3.202778,73.22068,462
Maldives,MDV,2009,22.92336887,25.0010029,3.202778,73.22068,462
Maldives,MDV,2010,20.32204842,24.94451793,3.202778,73.22068,462
Maldives,MDV,2011,17.97212946,24.25044692,3.202778,73.22068,462
Maldives,MDV,2012,15.9821241,23.01925194,3.202778,73.22068,462
Maldives,MDV,2013,14.25056275,21.26198963,3.202778,73.22068,462
Maldives,MDV,2014,12.76729414,19.43667,3.202778,73.22068,462
Maldives,MDV,2015,11.48504869,19.09381351,3.202778,73.22068,462
Maldives,MDV,2016,10.7384472,19.92471782,3.202778,73.22068,462
Maldives,MDV,2017,10.05227346,21.33774392,3.202778,73.22068,462
Maldives,MDV,2018,9.26401786,21.7659783,3.202778,73.22068,462
Maldives,MDV,2019,8.4090279,21.92332482,3.202778,73.22068,462
Mali,MLI,1990,238.0546239,16.609391,17.570692,-3.996166,466
Mali,MLI,1991,234.1569641,16.4586685,17.570692,-3.996166,466
Mali,MLI,1992,232.0533706,16.3756252,17.570692,-3.996166,466
Mali,MLI,1993,228.9085782,16.30448475,17.570692,-3.996166,466
Mali,MLI,1994,226.4336102,16.15913212,17.570692,-3.996166,466
Mali,MLI,1995,224.2819733,16.2138937,17.570692,-3.996166,466
Mali,MLI,1996,221.6596206,16.47321516,17.570692,-3.996166,466
Mali,MLI,1997,218.095077,17.06104833,17.570692,-3.996166,466
Mali,MLI,1998,213.3681361,17.59711291,17.570692,-3.996166,466
Mali,MLI,1999,208.4824805,18.02482178,17.570692,-3.996166,466
Mali,MLI,2000,205.353972,18.13943539,17.570692,-3.996166,466
Mali,MLI,2001,200.1977947,18.04909476,17.570692,-3.996166,466
Mali,MLI,2002,199.0532046,18.24790124,17.570692,-3.996166,466
Mali,MLI,2003,194.7337329,18.35112126,17.570692,-3.996166,466
Mali,MLI,2004,191.4949197,18.6259116,17.570692,-3.996166,466
Mali,MLI,2005,188.449406,19.16363731,17.570692,-3.996166,466
Mali,MLI,2006,186.2615338,19.86012765,17.570692,-3.996166,466
Mali,MLI,2007,183.9297252,20.34183379,17.570692,-3.996166,466
Mali,MLI,2008,182.9402033,20.65073563,17.570692,-3.996166,466
Mali,MLI,2009,181.3659009,21.11238594,17.570692,-3.996166,466
Mali,MLI,2010,178.6693853,21.81086281,17.570692,-3.996166,466
Mali,MLI,2011,174.8153683,22.55871085,17.570692,-3.996166,466
Mali,MLI,2012,171.5387334,23.45152892,17.570692,-3.996166,466
Mali,MLI,2013,168.4287,24.43237906,17.570692,-3.996166,466
Mali,MLI,2014,165.3358596,25.09217225,17.570692,-3.996166,466
Mali,MLI,2015,164.9169812,25.60854395,17.570692,-3.996166,466
Mali,MLI,2016,164.9701004,25.5227955,17.570692,-3.996166,466
Mali,MLI,2017,163.2334563,25.20030078,17.570692,-3.996166,466
Mali,MLI,2018,160.0544027,25.90854246,17.570692,-3.996166,466
Mali,MLI,2019,156.1247343,26.19685617,17.570692,-3.996166,466
Malta,MLT,1990,1.0066457,45.62544872,35.937496,14.375416,470
Malta,MLT,1991,0.901544407,44.37878663,35.937496,14.375416,470
Malta,MLT,1992,0.81075375,43.39608758,35.937496,14.375416,470
Malta,MLT,1993,0.717395872,41.95855403,35.937496,14.375416,470
Malta,MLT,1994,0.631182872,40.09494943,35.937496,14.375416,470
Malta,MLT,1995,0.56632941,39.17306182,35.937496,14.375416,470
Malta,MLT,1996,0.508451618,38.26874855,35.937496,14.375416,470
Malta,MLT,1997,0.454707014,37.5481107,35.937496,14.375416,470
Malta,MLT,1998,0.401924788,36.04017666,35.937496,14.375416,470
Malta,MLT,1999,0.363391491,35.44618746,35.937496,14.375416,470
Malta,MLT,2000,0.323173008,33.96965778,35.937496,14.375416,470
Malta,MLT,2001,0.287582426,32.75536035,35.937496,14.375416,470
Malta,MLT,2002,0.258286667,32.03688629,35.937496,14.375416,470
Malta,MLT,2003,0.229182235,30.86398727,35.937496,14.375416,470
Malta,MLT,2004,0.199148149,29.25678135,35.937496,14.375416,470
Malta,MLT,2005,0.173041039,27.70836753,35.937496,14.375416,470
Malta,MLT,2006,0.151628882,26.95533472,35.937496,14.375416,470
Malta,MLT,2007,0.133938732,27.0855535,35.937496,14.375416,470
Malta,MLT,2008,0.118589338,27.44002776,35.937496,14.375416,470
Malta,MLT,2009,0.104651748,27.43601847,35.937496,14.375416,470
Malta,MLT,2010,0.092898683,27.04665277,35.937496,14.375416,470
Malta,MLT,2011,0.085135312,26.2891512,35.937496,14.375416,470
Malta,MLT,2012,0.077971469,24.57659236,35.937496,14.375416,470
Malta,MLT,2013,0.071053989,22.45556054,35.937496,14.375416,470
Malta,MLT,2014,0.064942373,20.34232302,35.937496,14.375416,470
Malta,MLT,2015,0.05838331,18.25840856,35.937496,14.375416,470
Malta,MLT,2016,0.053722422,17.08371942,35.937496,14.375416,470
Malta,MLT,2017,0.049096713,16.25362489,35.937496,14.375416,470
Malta,MLT,2018,0.045124673,16.41885763,35.937496,14.375416,470
Malta,MLT,2019,0.041615699,16.7941461,35.937496,14.375416,470
Marshall Islands,MHL,1990,171.3439625,21.93151557,7.131474,171.184478,584
Marshall Islands,MHL,1991,166.5463906,23.14942951,7.131474,171.184478,584
Marshall Islands,MHL,1992,161.838521,24.40154587,7.131474,171.184478,584
Marshall Islands,MHL,1993,154.715341,25.15931938,7.131474,171.184478,584
Marshall Islands,MHL,1994,139.9047049,24.23422863,7.131474,171.184478,584
Marshall Islands,MHL,1995,136.3518047,25.42509323,7.131474,171.184478,584
Marshall Islands,MHL,1996,132.2147116,26.523151,7.131474,171.184478,584
Marshall Islands,MHL,1997,129.1041293,27.90284532,7.131474,171.184478,584
Marshall Islands,MHL,1998,125.4656111,29.11938699,7.131474,171.184478,584
Marshall Islands,MHL,1999,122.2118743,30.27649446,7.131474,171.184478,584
Marshall Islands,MHL,2000,119.1833097,31.26910641,7.131474,171.184478,584
Marshall Islands,MHL,2001,115.831495,32.13960384,7.131474,171.184478,584
Marshall Islands,MHL,2002,112.300819,33.0141812,7.131474,171.184478,584
Marshall Islands,MHL,2003,109.1464503,33.83012163,7.131474,171.184478,584
Marshall Islands,MHL,2004,106.6272564,34.45629001,7.131474,171.184478,584
Marshall Islands,MHL,2005,105.6527511,34.98610813,7.131474,171.184478,584
Marshall Islands,MHL,2006,106.4379034,35.62537857,7.131474,171.184478,584
Marshall Islands,MHL,2007,106.5689347,35.82087448,7.131474,171.184478,584
Marshall Islands,MHL,2008,106.7824371,35.93824904,7.131474,171.184478,584
Marshall Islands,MHL,2009,106.6349774,35.96819527,7.131474,171.184478,584
Marshall Islands,MHL,2010,105.9648892,35.91150946,7.131474,171.184478,584
Marshall Islands,MHL,2011,104.2973791,35.76615124,7.131474,171.184478,584
Marshall Islands,MHL,2012,101.4327959,35.5074113,7.131474,171.184478,584
Marshall Islands,MHL,2013,97.89265288,35.23971154,7.131474,171.184478,584
Marshall Islands,MHL,2014,94.10706244,35.04476007,7.131474,171.184478,584
Marshall Islands,MHL,2015,90.4860791,35.00747562,7.131474,171.184478,584
Marshall Islands,MHL,2016,86.35444344,35.65267585,7.131474,171.184478,584
Marshall Islands,MHL,2017,81.80464653,36.37824327,7.131474,171.184478,584
Marshall Islands,MHL,2018,77.4865931,36.60749104,7.131474,171.184478,584
Marshall Islands,MHL,2019,73.07067683,36.62953973,7.131474,171.184478,584
Mauritania,MRT,1990,182.5312081,47.77751189,21.00789,-10.940835,478
Mauritania,MRT,1991,174.7088773,49.19582591,21.00789,-10.940835,478
Mauritania,MRT,1992,168.4768314,50.8383139,21.00789,-10.940835,478
Mauritania,MRT,1993,162.2919941,52.22426373,21.00789,-10.940835,478
Mauritania,MRT,1994,153.6907198,52.48062146,21.00789,-10.940835,478
Mauritania,MRT,1995,146.0531895,52.77164461,21.00789,-10.940835,478
Mauritania,MRT,1996,141.2870244,53.99841204,21.00789,-10.940835,478
Mauritania,MRT,1997,135.6073309,54.88868691,21.00789,-10.940835,478
Mauritania,MRT,1998,131.1790336,55.96121621,21.00789,-10.940835,478
Mauritania,MRT,1999,124.5379651,55.4103061,21.00789,-10.940835,478
Mauritania,MRT,2000,121.136639,55.44714406,21.00789,-10.940835,478
Mauritania,MRT,2001,118.4669801,55.27539447,21.00789,-10.940835,478
Mauritania,MRT,2002,115.3756625,54.65329338,21.00789,-10.940835,478
Mauritania,MRT,2003,111.071106,53.45235983,21.00789,-10.940835,478
Mauritania,MRT,2004,109.2587165,53.55201553,21.00789,-10.940835,478
Mauritania,MRT,2005,106.1661776,53.29548049,21.00789,-10.940835,478
Mauritania,MRT,2006,103.3627144,53.83031621,21.00789,-10.940835,478
Mauritania,MRT,2007,97.94595747,53.47326106,21.00789,-10.940835,478
Mauritania,MRT,2008,93.2582139,53.78623521,21.00789,-10.940835,478
Mauritania,MRT,2009,91.11399719,55.89832713,21.00789,-10.940835,478
Mauritania,MRT,2010,86.71491285,56.77510413,21.00789,-10.940835,478
Mauritania,MRT,2011,83.19623369,58.67775593,21.00789,-10.940835,478
Mauritania,MRT,2012,80.55633402,61.89163775,21.00789,-10.940835,478
Mauritania,MRT,2013,76.42290546,64.19085056,21.00789,-10.940835,478
Mauritania,MRT,2014,70.69658648,64.47924581,21.00789,-10.940835,478
Mauritania,MRT,2015,67.25689847,65.82551395,21.00789,-10.940835,478
Mauritania,MRT,2016,62.56189248,64.90519346,21.00789,-10.940835,478
Mauritania,MRT,2017,60.03595611,65.70938011,21.00789,-10.940835,478
Mauritania,MRT,2018,56.74405783,65.86790383,21.00789,-10.940835,478
Mauritania,MRT,2019,53.98576704,65.8649983,21.00789,-10.940835,478
Mauritius,MUS,1990,21.62429515,52.45395775,21.00789,-10.940835,480
Mauritius,MUS,1991,19.02578591,51.5124859,21.00789,-10.940835,480
Mauritius,MUS,1992,17.42273226,52.37913932,21.00789,-10.940835,480
Mauritius,MUS,1993,15.94932933,53.91284008,21.00789,-10.940835,480
Mauritius,MUS,1994,14.47440361,54.39909052,21.00789,-10.940835,480
Mauritius,MUS,1995,12.92877964,53.83855774,21.00789,-10.940835,480
Mauritius,MUS,1996,11.70997594,53.97145929,21.00789,-10.940835,480
Mauritius,MUS,1997,10.99346758,55.97740929,21.00789,-10.940835,480
Mauritius,MUS,1998,9.520375766,53.36948662,21.00789,-10.940835,480
Mauritius,MUS,1999,8.570716903,52.90336386,21.00789,-10.940835,480
Mauritius,MUS,2000,7.605376621,51.68049671,21.00789,-10.940835,480
Mauritius,MUS,2001,6.696515157,51.26653635,21.00789,-10.940835,480
Mauritius,MUS,2002,5.95573739,52.31278093,21.00789,-10.940835,480
Mauritius,MUS,2003,5.29665737,52.87679465,21.00789,-10.940835,480
Mauritius,MUS,2004,4.589600344,51.97312572,21.00789,-10.940835,480
Mauritius,MUS,2005,4.124880833,51.85701351,21.00789,-10.940835,480
Mauritius,MUS,2006,3.682597884,49.96277923,21.00789,-10.940835,480
Mauritius,MUS,2007,3.206111913,46.48500629,21.00789,-10.940835,480
Mauritius,MUS,2008,2.935715951,45.27549012,21.00789,-10.940835,480
Mauritius,MUS,2009,2.658368003,43.86255064,21.00789,-10.940835,480
Mauritius,MUS,2010,2.365735086,41.92495199,21.00789,-10.940835,480
Mauritius,MUS,2011,2.060947505,40.21294086,21.00789,-10.940835,480
Mauritius,MUS,2012,1.860244865,39.78934866,21.00789,-10.940835,480
Mauritius,MUS,2013,1.614226485,38.47903251,21.00789,-10.940835,480
Mauritius,MUS,2014,1.457001739,38.47750732,21.00789,-10.940835,480
Mauritius,MUS,2015,1.28952938,37.69176415,21.00789,-10.940835,480
Mauritius,MUS,2016,1.168152919,37.24746796,21.00789,-10.940835,480
Mauritius,MUS,2017,1.074355485,36.93393327,21.00789,-10.940835,480
Mauritius,MUS,2018,0.979055625,37.11281179,21.00789,-10.940835,480
Mauritius,MUS,2019,0.876716474,36.9923388,21.00789,-10.940835,480
Mexico,MEX,1990,34.59903429,53.7687853,23.634501,-102.552784,484
Mexico,MEX,1991,32.53703873,53.22283445,23.634501,-102.552784,484
Mexico,MEX,1992,31.00573271,53.2378223,23.634501,-102.552784,484
Mexico,MEX,1993,29.60168158,53.04444801,23.634501,-102.552784,484
Mexico,MEX,1994,28.0404074,53.06792429,23.634501,-102.552784,484
Mexico,MEX,1995,26.99387089,53.5264775,23.634501,-102.552784,484
Mexico,MEX,1996,25.46726849,53.18204069,23.634501,-102.552784,484
Mexico,MEX,1997,23.80705204,52.77337702,23.634501,-102.552784,484
Mexico,MEX,1998,21.90091495,51.57009444,23.634501,-102.552784,484
Mexico,MEX,1999,19.93790175,50.23056787,23.634501,-102.552784,484
Mexico,MEX,2000,18.35012386,47.46513363,23.634501,-102.552784,484
Mexico,MEX,2001,17.42497628,45.37425342,23.634501,-102.552784,484
Mexico,MEX,2002,17.07322275,43.77139917,23.634501,-102.552784,484
Mexico,MEX,2003,16.64641419,41.80237323,23.634501,-102.552784,484
Mexico,MEX,2004,15.8418741,39.05395453,23.634501,-102.552784,484
Mexico,MEX,2005,15.49197479,38.25956538,23.634501,-102.552784,484
Mexico,MEX,2006,14.73018275,36.74679063,23.634501,-102.552784,484
Mexico,MEX,2007,14.23587462,35.28189715,23.634501,-102.552784,484
Mexico,MEX,2008,14.29921111,35.72195076,23.634501,-102.552784,484
Mexico,MEX,2009,14.28166815,35.98819949,23.634501,-102.552784,484
Mexico,MEX,2010,13.62503938,35.47717135,23.634501,-102.552784,484
Mexico,MEX,2011,12.99166609,34.75008576,23.634501,-102.552784,484
Mexico,MEX,2012,12.54188721,35.32124388,23.634501,-102.552784,484
Mexico,MEX,2013,12.42672431,36.79357761,23.634501,-102.552784,484
Mexico,MEX,2014,11.99661673,37.23637249,23.634501,-102.552784,484
Mexico,MEX,2015,11.51952066,36.62368918,23.634501,-102.552784,484
Mexico,MEX,2016,10.85801161,35.76444842,23.634501,-102.552784,484
Mexico,MEX,2017,10.30223951,35.45303097,23.634501,-102.552784,484
Mexico,MEX,2018,9.587664576,34.94057047,23.634501,-102.552784,484
Mexico,MEX,2019,8.999261862,35.27987294,23.634501,-102.552784,484
Micronesia (country),FSM,1990,218.7905085,28.28526623,7.425554,150.550812,583
Micronesia (country),FSM,1991,212.204042,29.55754203,7.425554,150.550812,583
Micronesia (country),FSM,1992,205.3334341,30.71952341,7.425554,150.550812,583
Micronesia (country),FSM,1993,198.369615,31.76037513,7.425554,150.550812,583
Micronesia (country),FSM,1994,191.9878397,32.77634868,7.425554,150.550812,583
Micronesia (country),FSM,1995,185.4408898,33.71748069,7.425554,150.550812,583
Micronesia (country),FSM,1996,179.7354688,34.87775993,7.425554,150.550812,583
Micronesia (country),FSM,1997,174.358494,35.81442107,7.425554,150.550812,583
Micronesia (country),FSM,1998,168.8016512,36.59405806,7.425554,150.550812,583
Micronesia (country),FSM,1999,163.3254551,37.11898108,7.425554,150.550812,583
Micronesia (country),FSM,2000,157.7146876,37.72634153,7.425554,150.550812,583
Micronesia (country),FSM,2001,151.9109707,38.32806338,7.425554,150.550812,583
Micronesia (country),FSM,2002,146.3163071,38.99409336,7.425554,150.550812,583
Micronesia (country),FSM,2003,140.7847002,39.64818532,7.425554,150.550812,583
Micronesia (country),FSM,2004,135.818353,40.31898058,7.425554,150.550812,583
Micronesia (country),FSM,2005,130.9714213,40.88228018,7.425554,150.550812,583
Micronesia (country),FSM,2006,126.1489043,41.28326885,7.425554,150.550812,583
Micronesia (country),FSM,2007,121.6778185,41.70597376,7.425554,150.550812,583
Micronesia (country),FSM,2008,117.5367737,42.17725458,7.425554,150.550812,583
Micronesia (country),FSM,2009,113.3226479,42.6516933,7.425554,150.550812,583
Micronesia (country),FSM,2010,109.0977281,43.15569957,7.425554,150.550812,583
Micronesia (country),FSM,2011,104.9653229,44.39672482,7.425554,150.550812,583
Micronesia (country),FSM,2012,100.8648187,46.41049745,7.425554,150.550812,583
Micronesia (country),FSM,2013,97.0755629,48.76630134,7.425554,150.550812,583
Micronesia (country),FSM,2014,93.55309845,50.80150646,7.425554,150.550812,583
Micronesia (country),FSM,2015,89.98499264,51.68265398,7.425554,150.550812,583
Micronesia (country),FSM,2016,86.2573224,49.05422148,7.425554,150.550812,583
Micronesia (country),FSM,2017,82.44278274,46.31322743,7.425554,150.550812,583
Micronesia (country),FSM,2018,78.76541491,46.80184129,7.425554,150.550812,583
Micronesia (country),FSM,2019,75.0527875,48.71198318,7.425554,150.550812,583
Moldova,MDA,1990,84.83999194,72.89815819,47.411631,28.369885,498
Moldova,MDA,1991,89.06652416,77.67630669,47.411631,28.369885,498
Moldova,MDA,1992,84.74705946,74.77405593,47.411631,28.369885,498
Moldova,MDA,1993,87.08263091,77.94623327,47.411631,28.369885,498
Moldova,MDA,1994,94.83777554,86.38849858,47.411631,28.369885,498
Moldova,MDA,1995,95.17247963,88.29109533,47.411631,28.369885,498
Moldova,MDA,1996,88.25433999,82.37177059,47.411631,28.369885,498
Moldova,MDA,1997,79.05178602,74.08768101,47.411631,28.369885,498
Moldova,MDA,1998,72.75716139,68.59403315,47.411631,28.369885,498
Moldova,MDA,1999,70.7895206,67.87563244,47.411631,28.369885,498
Moldova,MDA,2000,67.65713326,66.50695402,47.411631,28.369885,498
Moldova,MDA,2001,61.82052458,65.8403257,47.411631,28.369885,498
Moldova,MDA,2002,56.29214207,69.66844083,47.411631,28.369885,498
Moldova,MDA,2003,48.45793545,72.48964417,47.411631,28.369885,498
Moldova,MDA,2004,38.70469513,71.96409696,47.411631,28.369885,498
Moldova,MDA,2005,32.89587005,73.44546124,47.411631,28.369885,498
Moldova,MDA,2006,27.12283795,71.58371513,47.411631,28.369885,498
Moldova,MDA,2007,22.81940746,71.46213759,47.411631,28.369885,498
Moldova,MDA,2008,18.71518822,70.44719622,47.411631,28.369885,498
Moldova,MDA,2009,15.55910385,69.32590974,47.411631,28.369885,498
Moldova,MDA,2010,13.56070819,69.40404251,47.411631,28.369885,498
Moldova,MDA,2011,10.66611364,60.46933837,47.411631,28.369885,498
Moldova,MDA,2012,9.358339659,58.03607346,47.411631,28.369885,498
Moldova,MDA,2013,8.093409841,53.85406786,47.411631,28.369885,498
Moldova,MDA,2014,7.572673911,53.27507748,47.411631,28.369885,498
Moldova,MDA,2015,7.133020589,52.4326167,47.411631,28.369885,498
Moldova,MDA,2016,6.444348009,45.47377919,47.411631,28.369885,498
Moldova,MDA,2017,5.705020915,38.51719327,47.411631,28.369885,498
Moldova,MDA,2018,5.352083613,37.95399481,47.411631,28.369885,498
Moldova,MDA,2019,4.985874316,37.67379278,47.411631,28.369885,498
Monaco,MCO,1990,0.067367789,18.31172206,43.750298,7.412841,498
Monaco,MCO,1991,0.060834624,17.11437711,43.750298,7.412841,498
Monaco,MCO,1992,0.055086912,16.24696907,43.750298,7.412841,498
Monaco,MCO,1993,0.05034905,15.77927365,43.750298,7.412841,498
Monaco,MCO,1994,0.046895861,15.79542724,43.750298,7.412841,498
Monaco,MCO,1995,0.044798894,15.7864399,43.750298,7.412841,498
Monaco,MCO,1996,0.043679584,17.06372354,43.750298,7.412841,498
Monaco,MCO,1997,0.042694101,20.20423464,43.750298,7.412841,498
Monaco,MCO,1998,0.041675455,23.54101976,43.750298,7.412841,498
Monaco,MCO,1999,0.040497006,25.97460504,43.750298,7.412841,498
Monaco,MCO,2000,0.039117135,26.44692249,43.750298,7.412841,498
Monaco,MCO,2001,0.037466573,25.81063295,43.750298,7.412841,498
Monaco,MCO,2002,0.03528675,25.46737154,43.750298,7.412841,498
Monaco,MCO,2003,0.032924049,25.11600916,43.750298,7.412841,498
Monaco,MCO,2004,0.030613311,25.02993524,43.750298,7.412841,498
Monaco,MCO,2005,0.028645957,24.54588991,43.750298,7.412841,498
Monaco,MCO,2006,0.026911736,24.1240044,43.750298,7.412841,498
Monaco,MCO,2007,0.025078224,23.49267293,43.750298,7.412841,498
Monaco,MCO,2008,0.023393379,23.15092073,43.750298,7.412841,498
Monaco,MCO,2009,0.02203197,22.90596494,43.750298,7.412841,498
Monaco,MCO,2010,0.020930072,22.68878736,43.750298,7.412841,498
Monaco,MCO,2011,0.020078793,22.20642562,43.750298,7.412841,498
Monaco,MCO,2012,0.019271419,21.61627234,43.750298,7.412841,498
Monaco,MCO,2013,0.018508619,20.84866541,43.750298,7.412841,498
Monaco,MCO,2014,0.017728933,20.13747812,43.750298,7.412841,498
Monaco,MCO,2015,0.016820841,19.09510782,43.750298,7.412841,498
Monaco,MCO,2016,0.015663168,17.4450694,43.750298,7.412841,498
Monaco,MCO,2017,0.014595076,16.0014642,43.750298,7.412841,498
Monaco,MCO,2018,0.013832014,15.78258882,43.750298,7.412841,498
Monaco,MCO,2019,0.013213059,15.73940594,43.750298,7.412841,498
Mongolia,MNG,1990,194.2032458,65.88320505,46.862496,103.846656,498
Mongolia,MNG,1991,193.8911971,67.72052613,46.862496,103.846656,498
Mongolia,MNG,1992,194.2061656,69.85216516,46.862496,103.846656,498
Mongolia,MNG,1993,190.4513003,71.01269661,46.862496,103.846656,498
Mongolia,MNG,1994,189.7694249,73.31747349,46.862496,103.846656,498
Mongolia,MNG,1995,196.8862573,79.15979048,46.862496,103.846656,498
Mongolia,MNG,1996,199.4649502,84.01235117,46.862496,103.846656,498
Mongolia,MNG,1997,196.2854552,87.23003483,46.862496,103.846656,498
Mongolia,MNG,1998,191.5813679,90.40364672,46.862496,103.846656,498
Mongolia,MNG,1999,189.5028067,94.19888914,46.862496,103.846656,498
Mongolia,MNG,2000,187.3865713,96.81870611,46.862496,103.846656,498
Mongolia,MNG,2001,183.1731099,98.1116608,46.862496,103.846656,498
Mongolia,MNG,2002,176.132525,97.13716228,46.862496,103.846656,498
Mongolia,MNG,2003,168.1318798,95.39554851,46.862496,103.846656,498
Mongolia,MNG,2004,158.2819101,92.6893349,46.862496,103.846656,498
Mongolia,MNG,2005,150.0609319,91.40774196,46.862496,103.846656,498
Mongolia,MNG,2006,140.3498414,90.941467,46.862496,103.846656,498
Mongolia,MNG,2007,127.5016864,90.45020591,46.862496,103.846656,498
Mongolia,MNG,2008,116.6243815,92.19350501,46.862496,103.846656,498
Mongolia,MNG,2009,109.0914352,96.75200748,46.862496,103.846656,498
Mongolia,MNG,2010,99.84928844,98.98352861,46.862496,103.846656,498
Mongolia,MNG,2011,90.97866209,101.0998964,46.862496,103.846656,498
Mongolia,MNG,2012,82.41787063,103.1685147,46.862496,103.846656,498
Mongolia,MNG,2013,73.39529473,103.7344145,46.862496,103.846656,498
Mongolia,MNG,2014,65.11497746,102.4596129,46.862496,103.846656,498
Mongolia,MNG,2015,59.62784005,101.5191576,46.862496,103.846656,498
Mongolia,MNG,2016,57.30258188,102.5952087,46.862496,103.846656,498
Mongolia,MNG,2017,54.81218253,102.5299141,46.862496,103.846656,498
Mongolia,MNG,2018,51.64714884,103.5131673,46.862496,103.846656,498
Mongolia,MNG,2019,48.99939334,108.0768441,46.862496,103.846656,498
Montenegro,MNE,1990,33.74950132,74.96048718,42.708678,19.37439,499
Montenegro,MNE,1991,32.41268977,72.09424779,42.708678,19.37439,499
Montenegro,MNE,1992,32.50606695,72.4512775,42.708678,19.37439,499
Montenegro,MNE,1993,33.77775123,75.80176053,42.708678,19.37439,499
Montenegro,MNE,1994,35.06961607,78.77030363,42.708678,19.37439,499
Montenegro,MNE,1995,35.31582467,79.66119879,42.708678,19.37439,499
Montenegro,MNE,1996,35.50664157,80.5188979,42.708678,19.37439,499
Montenegro,MNE,1997,35.65606468,81.92557197,42.708678,19.37439,499
Montenegro,MNE,1998,34.45023978,80.29968711,42.708678,19.37439,499
Montenegro,MNE,1999,33.125025,78.3878257,42.708678,19.37439,499
Montenegro,MNE,2000,32.06113587,77.07379389,42.708678,19.37439,499
Montenegro,MNE,2001,31.03661415,76.61908026,42.708678,19.37439,499
Montenegro,MNE,2002,29.70811615,76.24811364,42.708678,19.37439,499
Montenegro,MNE,2003,28.68122489,76.77658147,42.708678,19.37439,499
Montenegro,MNE,2004,27.56673006,76.80591325,42.708678,19.37439,499
Montenegro,MNE,2005,26.74228574,76.87682673,42.708678,19.37439,499
Montenegro,MNE,2006,26.09994059,76.71856864,42.708678,19.37439,499
Montenegro,MNE,2007,25.56635663,76.52598779,42.708678,19.37439,499
Montenegro,MNE,2008,24.89167208,75.89090508,42.708678,19.37439,499
Montenegro,MNE,2009,24.23029273,75.11314199,42.708678,19.37439,499
Montenegro,MNE,2010,23.44635334,73.60673152,42.708678,19.37439,499
Montenegro,MNE,2011,22.86002625,72.5404035,42.708678,19.37439,499
Montenegro,MNE,2012,22.27246573,70.96789089,42.708678,19.37439,499
Montenegro,MNE,2013,22.02460623,70.37647333,42.708678,19.37439,499
Montenegro,MNE,2014,21.90886785,69.96223096,42.708678,19.37439,499
Montenegro,MNE,2015,21.5750375,68.99361789,42.708678,19.37439,499
Montenegro,MNE,2016,20.88703522,67.0152458,42.708678,19.37439,499
Montenegro,MNE,2017,20.17866295,65.02567118,42.708678,19.37439,499
Montenegro,MNE,2018,19.03783042,62.37907936,42.708678,19.37439,499
Montenegro,MNE,2019,17.7349229,60.02995867,42.708678,19.37439,499
Morocco,MAR,1990,75.85722632,51.71873742,31.791702,-7.09262,504
Morocco,MAR,1991,73.00365269,53.00891253,31.791702,-7.09262,504
Morocco,MAR,1992,71.26480369,55.52477377,31.791702,-7.09262,504
Morocco,MAR,1993,68.98922662,57.86083486,31.791702,-7.09262,504
Morocco,MAR,1994,65.33025534,58.84780888,31.791702,-7.09262,504
Morocco,MAR,1995,62.25688993,60.92361072,31.791702,-7.09262,504
Morocco,MAR,1996,58.68429775,62.78106058,31.791702,-7.09262,504
Morocco,MAR,1997,55.56788271,65.86951938,31.791702,-7.09262,504
Morocco,MAR,1998,52.2535166,68.89924502,31.791702,-7.09262,504
Morocco,MAR,1999,49.57855049,72.6551985,31.791702,-7.09262,504
Morocco,MAR,2000,45.0208125,72.03775678,31.791702,-7.09262,504
Morocco,MAR,2001,41.35279874,71.70208358,31.791702,-7.09262,504
Morocco,MAR,2002,38.38119044,72.15399767,31.791702,-7.09262,504
Morocco,MAR,2003,36.42469756,74.91700965,31.791702,-7.09262,504
Morocco,MAR,2004,33.88187645,76.14646496,31.791702,-7.09262,504
Morocco,MAR,2005,31.50912811,77.75077608,31.791702,-7.09262,504
Morocco,MAR,2006,29.11373322,79.74760582,31.791702,-7.09262,504
Morocco,MAR,2007,26.72723246,81.82840802,31.791702,-7.09262,504
Morocco,MAR,2008,24.16858459,83.14043542,31.791702,-7.09262,504
Morocco,MAR,2009,21.71097618,84.22372494,31.791702,-7.09262,504
Morocco,MAR,2010,19.44038028,84.8363914,31.791702,-7.09262,504
Morocco,MAR,2011,17.34122266,84.98347404,31.791702,-7.09262,504
Morocco,MAR,2012,15.49751191,85.5583941,31.791702,-7.09262,504
Morocco,MAR,2013,14.64672947,93.20856491,31.791702,-7.09262,504
Morocco,MAR,2014,12.8656038,93.2838146,31.791702,-7.09262,504
Morocco,MAR,2015,11.2131677,93.69117477,31.791702,-7.09262,504
Morocco,MAR,2016,9.673247193,95.57887421,31.791702,-7.09262,504
Morocco,MAR,2017,8.314175607,98.00696807,31.791702,-7.09262,504
Morocco,MAR,2018,7.118908985,99.60182253,31.791702,-7.09262,504
Morocco,MAR,2019,6.058518871,100.0942133,31.791702,-7.09262,504
Mozambique,MOZ,1990,251.0234148,6.686930251,-18.665695,35.529562,508
Mozambique,MOZ,1991,247.494901,6.650751627,-18.665695,35.529562,508
Mozambique,MOZ,1992,244.1211675,6.601805442,-18.665695,35.529562,508
Mozambique,MOZ,1993,239.1278481,6.555230223,-18.665695,35.529562,508
Mozambique,MOZ,1994,234.5643301,6.505284157,-18.665695,35.529562,508
Mozambique,MOZ,1995,232.5789271,6.577671908,-18.665695,35.529562,508
Mozambique,MOZ,1996,229.995745,6.70330382,-18.665695,35.529562,508
Mozambique,MOZ,1997,227.2383187,6.981746831,-18.665695,35.529562,508
Mozambique,MOZ,1998,223.9627723,7.27799119,-18.665695,35.529562,508
Mozambique,MOZ,1999,221.2940942,7.62138348,-18.665695,35.529562,508
Mozambique,MOZ,2000,220.3697528,7.861245561,-18.665695,35.529562,508
Mozambique,MOZ,2001,213.7523918,7.916191131,-18.665695,35.529562,508
Mozambique,MOZ,2002,212.0477843,8.055359871,-18.665695,35.529562,508
Mozambique,MOZ,2003,208.6558975,8.181386089,-18.665695,35.529562,508
Mozambique,MOZ,2004,208.5463988,8.583110253,-18.665695,35.529562,508
Mozambique,MOZ,2005,209.2650913,9.238514791,-18.665695,35.529562,508
Mozambique,MOZ,2006,211.8083042,10.34351232,-18.665695,35.529562,508
Mozambique,MOZ,2007,211.3976065,10.85644092,-18.665695,35.529562,508
Mozambique,MOZ,2008,212.6837185,11.32617699,-18.665695,35.529562,508
Mozambique,MOZ,2009,212.4346338,11.73018152,-18.665695,35.529562,508
Mozambique,MOZ,2010,213.293015,12.46746357,-18.665695,35.529562,508
Mozambique,MOZ,2011,212.9490182,13.40922654,-18.665695,35.529562,508
Mozambique,MOZ,2012,212.5432488,14.45674654,-18.665695,35.529562,508
Mozambique,MOZ,2013,209.8709541,15.34610875,-18.665695,35.529562,508
Mozambique,MOZ,2014,205.8457504,15.56071344,-18.665695,35.529562,508
Mozambique,MOZ,2015,202.1167514,15.64176824,-18.665695,35.529562,508
Mozambique,MOZ,2016,196.7835778,15.44135402,-18.665695,35.529562,508
Mozambique,MOZ,2017,192.452065,15.32044606,-18.665695,35.529562,508
Mozambique,MOZ,2018,188.8262131,15.3628772,-18.665695,35.529562,508
Mozambique,MOZ,2019,185.4592644,15.27873497,-18.665695,35.529562,508
Myanmar,MMR,1990,317.5233137,43.50031852,21.913965,95.956223,104
Myanmar,MMR,1991,315.9506096,44.50810344,21.913965,95.956223,104
Myanmar,MMR,1992,313.0789399,45.35241915,21.913965,95.956223,104
Myanmar,MMR,1993,309.6732944,46.10115137,21.913965,95.956223,104
Myanmar,MMR,1994,305.4158524,46.56583801,21.913965,95.956223,104
Myanmar,MMR,1995,301.0986676,46.99923467,21.913965,95.956223,104
Myanmar,MMR,1996,296.2182544,47.48801389,21.913965,95.956223,104
Myanmar,MMR,1997,290.6590091,47.91794887,21.913965,95.956223,104
Myanmar,MMR,1998,284.9200641,48.56586821,21.913965,95.956223,104
Myanmar,MMR,1999,278.2539295,48.9755759,21.913965,95.956223,104
Myanmar,MMR,2000,271.0426257,49.04283488,21.913965,95.956223,104
Myanmar,MMR,2001,262.1821245,50.00096357,21.913965,95.956223,104
Myanmar,MMR,2002,251.8988801,52.46365701,21.913965,95.956223,104
Myanmar,MMR,2003,241.1083395,55.6937201,21.913965,95.956223,104
Myanmar,MMR,2004,231.1227994,58.70670136,21.913965,95.956223,104
Myanmar,MMR,2005,219.5717236,60.30278154,21.913965,95.956223,104
Myanmar,MMR,2006,208.888141,62.77258904,21.913965,95.956223,104
Myanmar,MMR,2007,196.7495464,65.09424959,21.913965,95.956223,104
Myanmar,MMR,2008,186.0556354,66.59463726,21.913965,95.956223,104
Myanmar,MMR,2009,176.9236872,66.32468941,21.913965,95.956223,104
Myanmar,MMR,2010,167.8770924,65.94738213,21.913965,95.956223,104
Myanmar,MMR,2011,160.9673009,66.31175309,21.913965,95.956223,104
Myanmar,MMR,2012,154.2110975,66.23609902,21.913965,95.956223,104
Myanmar,MMR,2013,149.2399682,65.90526171,21.913965,95.956223,104
Myanmar,MMR,2014,144.1625392,63.93612105,21.913965,95.956223,104
Myanmar,MMR,2015,139.6932915,62.75347912,21.913965,95.956223,104
Myanmar,MMR,2016,135.2254685,61.26852056,21.913965,95.956223,104
Myanmar,MMR,2017,130.5934405,60.4830442,21.913965,95.956223,104
Myanmar,MMR,2018,125.3792191,62.02118711,21.913965,95.956223,104
Myanmar,MMR,2019,119.7245862,63.7235948,21.913965,95.956223,104
Namibia,NAM,1990,166.4411676,43.15704753,-22.95764,18.49041,516
Namibia,NAM,1991,161.6450161,43.83886328,-22.95764,18.49041,516
Namibia,NAM,1992,157.7369793,44.27284305,-22.95764,18.49041,516
Namibia,NAM,1993,153.5066748,44.89396018,-22.95764,18.49041,516
Namibia,NAM,1994,150.9921055,45.83375542,-22.95764,18.49041,516
Namibia,NAM,1995,148.1675119,47.11419084,-22.95764,18.49041,516
Namibia,NAM,1996,144.9183174,48.48581314,-22.95764,18.49041,516
Namibia,NAM,1997,142.5536725,50.70304486,-22.95764,18.49041,516
Namibia,NAM,1998,141.6140343,53.43322178,-22.95764,18.49041,516
Namibia,NAM,1999,141.170339,56.36383289,-22.95764,18.49041,516
Namibia,NAM,2000,141.1687824,58.04364318,-22.95764,18.49041,516
Namibia,NAM,2001,136.9956599,58.20580599,-22.95764,18.49041,516
Namibia,NAM,2002,135.7407176,58.99838503,-22.95764,18.49041,516
Namibia,NAM,2003,131.6432565,59.20452541,-22.95764,18.49041,516
Namibia,NAM,2004,126.2508691,59.58915154,-22.95764,18.49041,516
Namibia,NAM,2005,120.1144177,59.93676444,-22.95764,18.49041,516
Namibia,NAM,2006,112.8093639,60.2774491,-22.95764,18.49041,516
Namibia,NAM,2007,106.0111271,59.70453006,-22.95764,18.49041,516
Namibia,NAM,2008,99.77449985,59.22301446,-22.95764,18.49041,516
Namibia,NAM,2009,94.48853697,59.23693271,-22.95764,18.49041,516
Namibia,NAM,2010,89.80224554,59.76739454,-22.95764,18.49041,516
Namibia,NAM,2011,83.7989341,59.60372181,-22.95764,18.49041,516
Namibia,NAM,2012,79.05031108,60.30524396,-22.95764,18.49041,516
Namibia,NAM,2013,74.99948446,61.51722081,-22.95764,18.49041,516
Namibia,NAM,2014,71.44144899,62.46978193,-22.95764,18.49041,516
Namibia,NAM,2015,68.35055774,62.70006434,-22.95764,18.49041,516
Namibia,NAM,2016,65.4694327,62.51929961,-22.95764,18.49041,516
Namibia,NAM,2017,62.5822326,61.94254943,-22.95764,18.49041,516
Namibia,NAM,2018,59.49921907,61.16296581,-22.95764,18.49041,516
Namibia,NAM,2019,56.27411251,60.653222,-22.95764,18.49041,516
Nauru,NRU,1990,63.31289868,30.34538759,-0.522778,166.931503,520
Nauru,NRU,1991,61.29207812,32.34295803,-0.522778,166.931503,520
Nauru,NRU,1992,59.4727783,34.04054382,-0.522778,166.931503,520
Nauru,NRU,1993,57.33655664,35.19862513,-0.522778,166.931503,520
Nauru,NRU,1994,55.79917322,36.25800276,-0.522778,166.931503,520
Nauru,NRU,1995,54.74404124,37.37069156,-0.522778,166.931503,520
Nauru,NRU,1996,53.71929359,37.67084233,-0.522778,166.931503,520
Nauru,NRU,1997,52.72675306,36.87968751,-0.522778,166.931503,520
Nauru,NRU,1998,51.49194466,35.42915648,-0.522778,166.931503,520
Nauru,NRU,1999,50.04361174,34.08356317,-0.522778,166.931503,520
Nauru,NRU,2000,48.28178993,33.28326201,-0.522778,166.931503,520
Nauru,NRU,2001,46.82840409,33.42614672,-0.522778,166.931503,520
Nauru,NRU,2002,45.00034431,33.39896114,-0.522778,166.931503,520
Nauru,NRU,2003,43.04098129,33.2970825,-0.522778,166.931503,520
Nauru,NRU,2004,40.99612958,33.08392665,-0.522778,166.931503,520
Nauru,NRU,2005,38.79602463,32.76214429,-0.522778,166.931503,520
Nauru,NRU,2006,36.34691815,32.2026303,-0.522778,166.931503,520
Nauru,NRU,2007,33.92631094,31.51468014,-0.522778,166.931503,520
Nauru,NRU,2008,31.23550807,30.53436012,-0.522778,166.931503,520
Nauru,NRU,2009,28.57835618,29.65208098,-0.522778,166.931503,520
Nauru,NRU,2010,25.8362546,28.73794829,-0.522778,166.931503,520
Nauru,NRU,2011,23.1483281,28.07836634,-0.522778,166.931503,520
Nauru,NRU,2012,20.587222,27.73566335,-0.522778,166.931503,520
Nauru,NRU,2013,18.06216675,27.39344072,-0.522778,166.931503,520
Nauru,NRU,2014,15.73943031,27.06900103,-0.522778,166.931503,520
Nauru,NRU,2015,13.86471477,27.00719982,-0.522778,166.931503,520
Nauru,NRU,2016,12.36522973,27.70325802,-0.522778,166.931503,520
Nauru,NRU,2017,11.10311417,28.23249842,-0.522778,166.931503,520
Nauru,NRU,2018,9.985818215,27.93966725,-0.522778,166.931503,520
Nauru,NRU,2019,8.992197855,27.42572305,-0.522778,166.931503,520
Nepal,NPL,1990,296.5681374,64.4064966,28.394857,84.124008,524
Nepal,NPL,1991,289.5889691,63.8918573,28.394857,84.124008,524
Nepal,NPL,1992,281.6278095,62.76519341,28.394857,84.124008,524
Nepal,NPL,1993,276.4981171,63.65023871,28.394857,84.124008,524
Nepal,NPL,1994,268.5519743,64.06517938,28.394857,84.124008,524
Nepal,NPL,1995,260.8223014,65.05881636,28.394857,84.124008,524
Nepal,NPL,1996,250.9545836,65.69081616,28.394857,84.124008,524
Nepal,NPL,1997,242.2388968,67.20119014,28.394857,84.124008,524
Nepal,NPL,1998,233.0502222,69.502217,28.394857,84.124008,524
Nepal,NPL,1999,224.1480632,72.12832255,28.394857,84.124008,524
Nepal,NPL,2000,216.6034838,73.41516912,28.394857,84.124008,524
Nepal,NPL,2001,208.6433999,72.89164634,28.394857,84.124008,524
Nepal,NPL,2002,201.3365871,72.86646125,28.394857,84.124008,524
Nepal,NPL,2003,194.9808404,75.45666597,28.394857,84.124008,524
Nepal,NPL,2004,189.9780004,77.98233752,28.394857,84.124008,524
Nepal,NPL,2005,185.8943805,80.91904794,28.394857,84.124008,524
Nepal,NPL,2006,181.5564893,83.9158678,28.394857,84.124008,524
Nepal,NPL,2007,176.6677493,88.99109518,28.394857,84.124008,524
Nepal,NPL,2008,170.9774351,91.93917549,28.394857,84.124008,524
Nepal,NPL,2009,165.2494357,94.31841489,28.394857,84.124008,524
Nepal,NPL,2010,159.3357542,96.33230717,28.394857,84.124008,524
Nepal,NPL,2011,154.1087363,102.5711328,28.394857,84.124008,524
Nepal,NPL,2012,148.066185,108.7708799,28.394857,84.124008,524
Nepal,NPL,2013,142.2550729,115.6524289,28.394857,84.124008,524
Nepal,NPL,2014,135.9214612,118.4770807,28.394857,84.124008,524
Nepal,NPL,2015,131.448897,120.8880826,28.394857,84.124008,524
Nepal,NPL,2016,127.7416968,122.1927222,28.394857,84.124008,524
Nepal,NPL,2017,124.2878188,123.0041232,28.394857,84.124008,524
Nepal,NPL,2018,119.4366872,124.1624808,28.394857,84.124008,524
Nepal,NPL,2019,113.2451206,128.842631,28.394857,84.124008,524
Netherlands,NLD,1990,0.210667041,43.9704782,52.132633,5.291266,528
Netherlands,NLD,1991,0.190140619,42.58880911,52.132633,5.291266,528
Netherlands,NLD,1992,0.172277916,41.20237155,52.132633,5.291266,528
Netherlands,NLD,1993,0.160032478,41.33938992,52.132633,5.291266,528
Netherlands,NLD,1994,0.143721935,39.88235588,52.132633,5.291266,528
Netherlands,NLD,1995,0.13205145,39.1889796,52.132633,5.291266,528
Netherlands,NLD,1996,0.12187237,37.9913192,52.132633,5.291266,528
Netherlands,NLD,1997,0.111439409,36.16796917,52.132633,5.291266,528
Netherlands,NLD,1998,0.103051925,35.1764927,52.132633,5.291266,528
Netherlands,NLD,1999,0.096054349,34.20002642,52.132633,5.291266,528
Netherlands,NLD,2000,0.088168761,33.066345,52.132633,5.291266,528
Netherlands,NLD,2001,0.079801941,31.35099636,52.132633,5.291266,528
Netherlands,NLD,2002,0.072420346,30.4916216,52.132633,5.291266,528
Netherlands,NLD,2003,0.064954826,28.99994044,52.132633,5.291266,528
Netherlands,NLD,2004,0.056556024,26.77717567,52.132633,5.291266,528
Netherlands,NLD,2005,0.050209805,25.16268874,52.132633,5.291266,528
Netherlands,NLD,2006,0.044283127,23.80313258,52.132633,5.291266,528
Netherlands,NLD,2007,0.038957079,22.77627012,52.132633,5.291266,528
Netherlands,NLD,2008,0.034858773,22.05823181,52.132633,5.291266,528
Netherlands,NLD,2009,0.031243064,21.43954412,52.132633,5.291266,528
Netherlands,NLD,2010,0.028366544,20.78342592,52.132633,5.291266,528
Netherlands,NLD,2011,0.025911422,19.6213832,52.132633,5.291266,528
Netherlands,NLD,2012,0.02400325,18.41413748,52.132633,5.291266,528
Netherlands,NLD,2013,0.022082483,16.93383843,52.132633,5.291266,528
Netherlands,NLD,2014,0.02029435,15.50505837,52.132633,5.291266,528
Netherlands,NLD,2015,0.019269068,14.86469275,52.132633,5.291266,528
Netherlands,NLD,2016,0.018351059,14.49159468,52.132633,5.291266,528
Netherlands,NLD,2017,0.017519182,14.2203541,52.132633,5.291266,528
Netherlands,NLD,2018,0.016680726,14.20014617,52.132633,5.291266,528
Netherlands,NLD,2019,0.01579993,13.93699274,52.132633,5.291266,528
New Zealand,NZL,1990,0.395122181,11.88262935,-40.900557,174.885971,554
New Zealand,NZL,1991,0.358201445,11.40658628,-40.900557,174.885971,554
New Zealand,NZL,1992,0.330967418,11.17898113,-40.900557,174.885971,554
New Zealand,NZL,1993,0.306799642,10.95190091,-40.900557,174.885971,554
New Zealand,NZL,1994,0.276960845,10.43465152,-40.900557,174.885971,554
New Zealand,NZL,1995,0.257593888,10.28361469,-40.900557,174.885971,554
New Zealand,NZL,1996,0.235910642,9.870495757,-40.900557,174.885971,554
New Zealand,NZL,1997,0.213943235,9.445525266,-40.900557,174.885971,554
New Zealand,NZL,1998,0.191465395,8.889195823,-40.900557,174.885971,554
New Zealand,NZL,1999,0.178304418,8.673377489,-40.900557,174.885971,554
New Zealand,NZL,2000,0.160393853,8.126239636,-40.900557,174.885971,554
New Zealand,NZL,2001,0.145644419,7.775022195,-40.900557,174.885971,554
New Zealand,NZL,2002,0.130444008,7.366749266,-40.900557,174.885971,554
New Zealand,NZL,2003,0.113936826,6.806339465,-40.900557,174.885971,554
New Zealand,NZL,2004,0.100305927,6.351265007,-40.900557,174.885971,554
New Zealand,NZL,2005,0.088126054,5.879643815,-40.900557,174.885971,554
New Zealand,NZL,2006,0.080153895,5.647183042,-40.900557,174.885971,554
New Zealand,NZL,2007,0.073589795,5.449965181,-40.900557,174.885971,554
New Zealand,NZL,2008,0.067596744,5.252716674,-40.900557,174.885971,554
New Zealand,NZL,2009,0.062036749,5.093336048,-40.900557,174.885971,554
New Zealand,NZL,2010,0.05704091,4.911669451,-40.900557,174.885971,554
New Zealand,NZL,2011,0.05277854,4.819050444,-40.900557,174.885971,554
New Zealand,NZL,2012,0.048433957,4.532488765,-40.900557,174.885971,554
New Zealand,NZL,2013,0.044365536,4.257750479,-40.900557,174.885971,554
New Zealand,NZL,2014,0.041920374,4.137891649,-40.900557,174.885971,554
New Zealand,NZL,2015,0.038455997,3.966128457,-40.900557,174.885971,554
New Zealand,NZL,2016,0.03558653,3.876621666,-40.900557,174.885971,554
New Zealand,NZL,2017,0.033908966,3.726491827,-40.900557,174.885971,554
New Zealand,NZL,2018,0.03353532,4.0334551,-40.900557,174.885971,554
New Zealand,NZL,2019,0.032497919,4.125173772,-40.900557,174.885971,554
Nicaragua,NIC,1990,92.72699337,11.1464766,12.865416,-85.207229,558
Nicaragua,NIC,1991,96.9680813,12.11739446,12.865416,-85.207229,558
Nicaragua,NIC,1992,92.37801036,12.08114643,12.865416,-85.207229,558
Nicaragua,NIC,1993,90.2752181,12.35919822,12.865416,-85.207229,558
Nicaragua,NIC,1994,87.66340764,12.79160316,12.865416,-85.207229,558
Nicaragua,NIC,1995,104.9724752,15.74097563,12.865416,-85.207229,558
Nicaragua,NIC,1996,104.014019,16.66178168,12.865416,-85.207229,558
Nicaragua,NIC,1997,95.19544402,16.3635462,12.865416,-85.207229,558
Nicaragua,NIC,1998,89.43894624,16.71590198,12.865416,-85.207229,558
Nicaragua,NIC,1999,86.5764102,17.79252365,12.865416,-85.207229,558
Nicaragua,NIC,2000,82.56559517,18.13882675,12.865416,-85.207229,558
Nicaragua,NIC,2001,82.13497672,19.40457023,12.865416,-85.207229,558
Nicaragua,NIC,2002,82.57291011,20.83356804,12.865416,-85.207229,558
Nicaragua,NIC,2003,81.63097863,22.15761423,12.865416,-85.207229,558
Nicaragua,NIC,2004,80.76932454,22.84271408,12.865416,-85.207229,558
Nicaragua,NIC,2005,81.23849274,24.11506768,12.865416,-85.207229,558
Nicaragua,NIC,2006,74.34456225,23.11588161,12.865416,-85.207229,558
Nicaragua,NIC,2007,74.93653533,24.22205005,12.865416,-85.207229,558
Nicaragua,NIC,2008,73.17673777,24.5512407,12.865416,-85.207229,558
Nicaragua,NIC,2009,70.07768426,24.43824491,12.865416,-85.207229,558
Nicaragua,NIC,2010,66.54838434,24.43381979,12.865416,-85.207229,558
Nicaragua,NIC,2011,64.10424463,25.35554733,12.865416,-85.207229,558
Nicaragua,NIC,2012,61.19883672,26.56173724,12.865416,-85.207229,558
Nicaragua,NIC,2013,58.57914339,27.0843157,12.865416,-85.207229,558
Nicaragua,NIC,2014,55.98974895,27.35969746,12.865416,-85.207229,558
Nicaragua,NIC,2015,53.35586324,26.95855078,12.865416,-85.207229,558
Nicaragua,NIC,2016,51.88910157,26.62386785,12.865416,-85.207229,558
Nicaragua,NIC,2017,49.66398813,25.42283816,12.865416,-85.207229,558
Nicaragua,NIC,2018,47.89258224,26.16032478,12.865416,-85.207229,558
Nicaragua,NIC,2019,45.4528378,27.14053412,12.865416,-85.207229,558
Niger,NER,1990,316.3516984,23.02854411,17.607789,8.081666,562
Niger,NER,1991,310.3187761,22.61552123,17.607789,8.081666,562
Niger,NER,1992,308.0470666,22.56379441,17.607789,8.081666,562
Niger,NER,1993,305.0123734,22.54220785,17.607789,8.081666,562
Niger,NER,1994,297.8372254,22.23395535,17.607789,8.081666,562
Niger,NER,1995,294.1620042,22.20749701,17.607789,8.081666,562
Niger,NER,1996,283.6359225,21.8781744,17.607789,8.081666,562
Niger,NER,1997,279.7536997,22.27248242,17.607789,8.081666,562
Niger,NER,1998,274.6548313,22.59273465,17.607789,8.081666,562
Niger,NER,1999,270.3137821,22.98588561,17.607789,8.081666,562
Niger,NER,2000,267.2831209,23.06712449,17.607789,8.081666,562
Niger,NER,2001,263.6387496,23.14398575,17.607789,8.081666,562
Niger,NER,2002,258.5821064,23.12657638,17.607789,8.081666,562
Niger,NER,2003,254.4361713,23.37960172,17.607789,8.081666,562
Niger,NER,2004,244.489098,23.04593861,17.607789,8.081666,562
Niger,NER,2005,243.2996197,23.43715745,17.607789,8.081666,562
Niger,NER,2006,236.8497366,23.3039967,17.607789,8.081666,562
Niger,NER,2007,231.7992833,23.00054687,17.607789,8.081666,562
Niger,NER,2008,223.2953627,22.05455768,17.607789,8.081666,562
Niger,NER,2009,220.3571622,21.69865684,17.607789,8.081666,562
Niger,NER,2010,217.3828561,21.67270957,17.607789,8.081666,562
Niger,NER,2011,216.6937694,22.36984287,17.607789,8.081666,562
Niger,NER,2012,214.3644219,23.50581804,17.607789,8.081666,562
Niger,NER,2013,212.3271207,25.05304707,17.607789,8.081666,562
Niger,NER,2014,209.112821,26.03999111,17.607789,8.081666,562
Niger,NER,2015,210.7375056,26.85357512,17.607789,8.081666,562
Niger,NER,2016,209.8961479,25.88388957,17.607789,8.081666,562
Niger,NER,2017,208.9627191,25.05830823,17.607789,8.081666,562
Niger,NER,2018,205.240171,25.63232817,17.607789,8.081666,562
Niger,NER,2019,199.5145858,26.26908991,17.607789,8.081666,562
Nigeria,NGA,1990,205.4073106,34.05958638,9.081999,8.675277,566
Nigeria,NGA,1991,203.8934584,34.1773345,9.081999,8.675277,566
Nigeria,NGA,1992,202.886881,34.38944033,9.081999,8.675277,566
Nigeria,NGA,1993,201.7619979,34.66303263,9.081999,8.675277,566
Nigeria,NGA,1994,200.3432206,34.90713132,9.081999,8.675277,566
Nigeria,NGA,1995,198.0556403,35.25525372,9.081999,8.675277,566
Nigeria,NGA,1996,196.6017618,35.99436762,9.081999,8.675277,566
Nigeria,NGA,1997,194.6811808,37.0664304,9.081999,8.675277,566
Nigeria,NGA,1998,192.6358917,38.31364649,9.081999,8.675277,566
Nigeria,NGA,1999,190.4237171,39.52573858,9.081999,8.675277,566
Nigeria,NGA,2000,187.5239199,40.1504917,9.081999,8.675277,566
Nigeria,NGA,2001,182.6088194,40.36509487,9.081999,8.675277,566
Nigeria,NGA,2002,177.3771654,41.10937084,9.081999,8.675277,566
Nigeria,NGA,2003,169.4349715,41.60937765,9.081999,8.675277,566
Nigeria,NGA,2004,161.6650259,42.21749215,9.081999,8.675277,566
Nigeria,NGA,2005,154.0497365,42.67621125,9.081999,8.675277,566
Nigeria,NGA,2006,149.2176615,43.65512942,9.081999,8.675277,566
Nigeria,NGA,2007,142.5123587,43.93125133,9.081999,8.675277,566
Nigeria,NGA,2008,136.3542723,44.47981766,9.081999,8.675277,566
Nigeria,NGA,2009,131.1509288,45.51726018,9.081999,8.675277,566
Nigeria,NGA,2010,125.5845407,47.18508505,9.081999,8.675277,566
Nigeria,NGA,2011,120.1768009,49.86553324,9.081999,8.675277,566
Nigeria,NGA,2012,115.2705283,53.66290513,9.081999,8.675277,566
Nigeria,NGA,2013,109.9077825,57.52825441,9.081999,8.675277,566
Nigeria,NGA,2014,104.2358321,59.71647673,9.081999,8.675277,566
Nigeria,NGA,2015,100.75079,61.34765647,9.081999,8.675277,566
Nigeria,NGA,2016,97.11183141,60.4350176,9.081999,8.675277,566
Nigeria,NGA,2017,93.06238804,59.5637101,9.081999,8.675277,566
Nigeria,NGA,2018,88.43165444,60.05701949,9.081999,8.675277,566
Nigeria,NGA,2019,83.22525882,61.69916752,9.081999,8.675277,566
Niue,NIU,1990,56.79941719,22.6320195,-19.054445,-169.867233,570
Niue,NIU,1991,54.00845442,23.32626264,-19.054445,-169.867233,570
Niue,NIU,1992,51.59538336,24.1856552,-19.054445,-169.867233,570
Niue,NIU,1993,48.37886894,24.66862053,-19.054445,-169.867233,570
Niue,NIU,1994,45.23272963,24.40683491,-19.054445,-169.867233,570
Niue,NIU,1995,42.4962016,24.29369284,-19.054445,-169.867233,570
Niue,NIU,1996,39.84597963,24.62570132,-19.054445,-169.867233,570
Niue,NIU,1997,37.26252548,25.44273273,-19.054445,-169.867233,570
Niue,NIU,1998,34.27279635,25.89534481,-19.054445,-169.867233,570
Niue,NIU,1999,31.60795085,26.07707114,-19.054445,-169.867233,570
Niue,NIU,2000,29.05264663,25.7087241,-19.054445,-169.867233,570
Niue,NIU,2001,26.45801919,25.42327787,-19.054445,-169.867233,570
Niue,NIU,2002,23.98755019,25.29214692,-19.054445,-169.867233,570
Niue,NIU,2003,21.59943485,25.04200076,-19.054445,-169.867233,570
Niue,NIU,2004,19.42117621,24.83521732,-19.054445,-169.867233,570
Niue,NIU,2005,17.32378155,24.52736723,-19.054445,-169.867233,570
Niue,NIU,2006,15.48492319,24.39856923,-19.054445,-169.867233,570
Niue,NIU,2007,13.61859089,23.70354015,-19.054445,-169.867233,570
Niue,NIU,2008,11.96133273,23.06266264,-19.054445,-169.867233,570
Niue,NIU,2009,10.3535277,21.99183156,-19.054445,-169.867233,570
Niue,NIU,2010,9.151856908,21.35011205,-19.054445,-169.867233,570
Niue,NIU,2011,8.280411648,21.02918473,-19.054445,-169.867233,570
Niue,NIU,2012,7.493577749,20.72226922,-19.054445,-169.867233,570
Niue,NIU,2013,6.830057572,20.77605204,-19.054445,-169.867233,570
Niue,NIU,2014,6.277377143,20.68520207,-19.054445,-169.867233,570
Niue,NIU,2015,5.834765267,20.75657891,-19.054445,-169.867233,570
Niue,NIU,2016,5.505440405,21.43031488,-19.054445,-169.867233,570
Niue,NIU,2017,5.210793538,22.08304927,-19.054445,-169.867233,570
Niue,NIU,2018,4.912460083,22.68680927,-19.054445,-169.867233,570
Niue,NIU,2019,4.610918019,22.76435117,-19.054445,-169.867233,570
North Korea,PRK,1990,213.9749558,62.71738196,40.339852,127.510093,408
North Korea,PRK,1991,212.1775791,63.1995513,40.339852,127.510093,408
North Korea,PRK,1992,210.6188134,64.12811467,40.339852,127.510093,408
North Korea,PRK,1993,209.6075361,64.7797236,40.339852,127.510093,408
North Korea,PRK,1994,208.6639451,65.08785626,40.339852,127.510093,408
North Korea,PRK,1995,207.9277276,65.85286398,40.339852,127.510093,408
North Korea,PRK,1996,207.1311348,67.20419678,40.339852,127.510093,408
North Korea,PRK,1997,206.1001274,69.40105263,40.339852,127.510093,408
North Korea,PRK,1998,204.4541404,71.31729841,40.339852,127.510093,408
North Korea,PRK,1999,202.5294158,72.54460557,40.339852,127.510093,408
North Korea,PRK,2000,199.8213144,71.40354701,40.339852,127.510093,408
North Korea,PRK,2001,196.477542,70.33903421,40.339852,127.510093,408
North Korea,PRK,2002,192.695441,70.15384811,40.339852,127.510093,408
North Korea,PRK,2003,188.6022628,71.65904619,40.339852,127.510093,408
North Korea,PRK,2004,184.4608922,73.25121172,40.339852,127.510093,408
North Korea,PRK,2005,180.417539,73.96819223,40.339852,127.510093,408
North Korea,PRK,2006,176.7415585,74.83345427,40.339852,127.510093,408
North Korea,PRK,2007,173.04494,75.43896721,40.339852,127.510093,408
North Korea,PRK,2008,169.323006,76.93938497,40.339852,127.510093,408
North Korea,PRK,2009,164.76858,77.24061916,40.339852,127.510093,408
North Korea,PRK,2010,159.528315,77.88086994,40.339852,127.510093,408
North Korea,PRK,2011,153.0725517,79.45220455,40.339852,127.510093,408
North Korea,PRK,2012,145.2428747,82.20852163,40.339852,127.510093,408
North Korea,PRK,2013,137.2779212,86.20909294,40.339852,127.510093,408
North Korea,PRK,2014,130.0158781,88.34677872,40.339852,127.510093,408
North Korea,PRK,2015,124.6756178,89.10435826,40.339852,127.510093,408
North Korea,PRK,2016,120.8800458,85.97140833,40.339852,127.510093,408
North Korea,PRK,2017,117.5730996,83.36304991,40.339852,127.510093,408
North Korea,PRK,2018,113.062468,84.01795213,40.339852,127.510093,408
North Korea,PRK,2019,107.2712192,86.24881821,40.339852,127.510093,408
North Macedonia,MKD,1990,64.99424297,119.5782551,41.608635,21.745275,807
North Macedonia,MKD,1991,63.48881676,118.928904,41.608635,21.745275,807
North Macedonia,MKD,1992,65.40593322,125.9567938,41.608635,21.745275,807
North Macedonia,MKD,1993,64.70023099,128.1119794,41.608635,21.745275,807
North Macedonia,MKD,1994,63.2236907,128.5684595,41.608635,21.745275,807
North Macedonia,MKD,1995,62.17916564,130.4800209,41.608635,21.745275,807
North Macedonia,MKD,1996,60.82380988,131.8001436,41.608635,21.745275,807
North Macedonia,MKD,1997,58.97630065,132.8200867,41.608635,21.745275,807
North Macedonia,MKD,1998,57.0580533,134.0611779,41.608635,21.745275,807
North Macedonia,MKD,1999,53.85929624,132.9482218,41.608635,21.745275,807
North Macedonia,MKD,2000,51.58822162,132.7252558,41.608635,21.745275,807
North Macedonia,MKD,2001,50.17817867,135.0001685,41.608635,21.745275,807
North Macedonia,MKD,2002,48.8658464,138.2049613,41.608635,21.745275,807
North Macedonia,MKD,2003,46.2352965,137.0523017,41.608635,21.745275,807
North Macedonia,MKD,2004,42.94855915,132.8739271,41.608635,21.745275,807
North Macedonia,MKD,2005,40.76377499,131.5558803,41.608635,21.745275,807
North Macedonia,MKD,2006,39.24986095,132.0995783,41.608635,21.745275,807
North Macedonia,MKD,2007,37.9031927,133.236391,41.608635,21.745275,807
North Macedonia,MKD,2008,35.22147556,129.0082394,41.608635,21.745275,807
North Macedonia,MKD,2009,33.32276604,127.2957379,41.608635,21.745275,807
North Macedonia,MKD,2010,31.23982327,123.539568,41.608635,21.745275,807
North Macedonia,MKD,2011,29.17246318,118.6626605,41.608635,21.745275,807
North Macedonia,MKD,2012,27.88913331,116.4371306,41.608635,21.745275,807
North Macedonia,MKD,2013,25.83292207,111.4275877,41.608635,21.745275,807
North Macedonia,MKD,2014,24.73078609,109.9507168,41.608635,21.745275,807
North Macedonia,MKD,2015,23.63748156,107.8743451,41.608635,21.745275,807
North Macedonia,MKD,2016,22.39085713,105.7151758,41.608635,21.745275,807
North Macedonia,MKD,2017,21.24685849,103.4475404,41.608635,21.745275,807
North Macedonia,MKD,2018,20.32692821,101.4819078,41.608635,21.745275,807
North Macedonia,MKD,2019,19.35470132,99.24804149,41.608635,21.745275,807
Northern Mariana Islands,MNP,1990,29.26074957,35.32888316,17.33083,145.38469,580
Northern Mariana Islands,MNP,1991,25.88550274,35.08778756,17.33083,145.38469,580
Northern Mariana Islands,MNP,1992,22.77279291,34.61437397,17.33083,145.38469,580
Northern Mariana Islands,MNP,1993,20.12750031,34.71946891,17.33083,145.38469,580
Northern Mariana Islands,MNP,1994,18.0409915,34.58353696,17.33083,145.38469,580
Northern Mariana Islands,MNP,1995,16.61589599,34.49544674,17.33083,145.38469,580
Northern Mariana Islands,MNP,1996,15.63934204,33.43058026,17.33083,145.38469,580
Northern Mariana Islands,MNP,1997,14.88336209,32.11243316,17.33083,145.38469,580
Northern Mariana Islands,MNP,1998,14.22117966,30.80114089,17.33083,145.38469,580
Northern Mariana Islands,MNP,1999,13.70928559,30.02511341,17.33083,145.38469,580
Northern Mariana Islands,MNP,2000,13.04644997,28.90910208,17.33083,145.38469,580
Northern Mariana Islands,MNP,2001,12.51312821,28.19442044,17.33083,145.38469,580
Northern Mariana Islands,MNP,2002,11.97497433,27.26975794,17.33083,145.38469,580
Northern Mariana Islands,MNP,2003,11.5579981,27.41659964,17.33083,145.38469,580
Northern Mariana Islands,MNP,2004,11.25610456,27.330459,17.33083,145.38469,580
Northern Mariana Islands,MNP,2005,11.15061747,27.56545214,17.33083,145.38469,580
Northern Mariana Islands,MNP,2006,11.13543776,26.90350257,17.33083,145.38469,580
Northern Mariana Islands,MNP,2007,11.26085234,26.0602689,17.33083,145.38469,580
Northern Mariana Islands,MNP,2008,11.52595097,25.40617554,17.33083,145.38469,580
Northern Mariana Islands,MNP,2009,11.90671931,24.67390329,17.33083,145.38469,580
Northern Mariana Islands,MNP,2010,12.1889073,24.03052523,17.33083,145.38469,580
Northern Mariana Islands,MNP,2011,12.70069401,24.34012419,17.33083,145.38469,580
Northern Mariana Islands,MNP,2012,13.37244824,26.44910542,17.33083,145.38469,580
Northern Mariana Islands,MNP,2013,14.08495547,29.20256483,17.33083,145.38469,580
Northern Mariana Islands,MNP,2014,14.61136314,31.40836845,17.33083,145.38469,580
Northern Mariana Islands,MNP,2015,14.83108182,32.26015618,17.33083,145.38469,580
Northern Mariana Islands,MNP,2016,14.27300284,28.74869326,17.33083,145.38469,580
Northern Mariana Islands,MNP,2017,13.29295558,25.39424183,17.33083,145.38469,580
Northern Mariana Islands,MNP,2018,12.35510855,25.08823896,17.33083,145.38469,580
Northern Mariana Islands,MNP,2019,11.29698829,25.6673728,17.33083,145.38469,580
Norway,NOR,1990,0.151976437,24.09586478,60.472024,8.468946,578
Norway,NOR,1991,0.136946895,22.6736591,60.472024,8.468946,578
Norway,NOR,1992,0.125208314,21.67640287,60.472024,8.468946,578
Norway,NOR,1993,0.114256061,20.90162646,60.472024,8.468946,578
Norway,NOR,1994,0.103014852,19.81829612,60.472024,8.468946,578
Norway,NOR,1995,0.093260589,19.0388201,60.472024,8.468946,578
Norway,NOR,1996,0.084633131,18.21935014,60.472024,8.468946,578
Norway,NOR,1997,0.077656999,17.56109386,60.472024,8.468946,578
Norway,NOR,1998,0.071828525,17.13593017,60.472024,8.468946,578
Norway,NOR,1999,0.066143903,16.48919998,60.472024,8.468946,578
Norway,NOR,2000,0.059812874,15.79004957,60.472024,8.468946,578
Norway,NOR,2001,0.053662984,14.76632618,60.472024,8.468946,578
Norway,NOR,2002,0.048167522,13.56681632,60.472024,8.468946,578
Norway,NOR,2003,0.041831356,11.97854265,60.472024,8.468946,578
Norway,NOR,2004,0.036523229,10.50769224,60.472024,8.468946,578
Norway,NOR,2005,0.032811916,9.701273308,60.472024,8.468946,578
Norway,NOR,2006,0.030189248,9.221860975,60.472024,8.468946,578
Norway,NOR,2007,0.028179236,9.067253803,60.472024,8.468946,578
Norway,NOR,2008,0.026037498,8.696090912,60.472024,8.468946,578
Norway,NOR,2009,0.023961197,8.431471286,60.472024,8.468946,578
Norway,NOR,2010,0.021956373,8.088965164,60.472024,8.468946,578
Norway,NOR,2011,0.020416072,7.868056596,60.472024,8.468946,578
Norway,NOR,2012,0.018524781,7.387395908,60.472024,8.468946,578
Norway,NOR,2013,0.016761927,6.745266737,60.472024,8.468946,578
Norway,NOR,2014,0.01487656,5.971551671,60.472024,8.468946,578
Norway,NOR,2015,0.013394965,5.315094955,60.472024,8.468946,578
Norway,NOR,2016,0.012034168,4.784883223,60.472024,8.468946,578
Norway,NOR,2017,0.010863388,4.25977528,60.472024,8.468946,578
Norway,NOR,2018,0.010517601,4.381687485,60.472024,8.468946,578
Norway,NOR,2019,0.010188878,4.357697822,60.472024,8.468946,578
Oman,OMN,1990,104.2532668,111.0861154,21.512583,55.923255,512
Oman,OMN,1991,90.64989529,117.3504312,21.512583,55.923255,512
Oman,OMN,1992,78.03057603,123.5498646,21.512583,55.923255,512
Oman,OMN,1993,66.4562629,129.4254211,21.512583,55.923255,512
Oman,OMN,1994,56.35119449,135.8391978,21.512583,55.923255,512
Oman,OMN,1995,47.43089853,141.7470844,21.512583,55.923255,512
Oman,OMN,1996,39.21839248,147.8312347,21.512583,55.923255,512
Oman,OMN,1997,31.43041063,154.0446585,21.512583,55.923255,512
Oman,OMN,1998,24.52205465,159.7121891,21.512583,55.923255,512
Oman,OMN,1999,18.89368168,163.9445493,21.512583,55.923255,512
Oman,OMN,2000,14.88670638,165.4904254,21.512583,55.923255,512
Oman,OMN,2001,11.73163355,160.5558814,21.512583,55.923255,512
Oman,OMN,2002,9.470577398,160.1978577,21.512583,55.923255,512
Oman,OMN,2003,7.559400815,158.7519077,21.512583,55.923255,512
Oman,OMN,2004,5.906544061,153.1541741,21.512583,55.923255,512
Oman,OMN,2005,4.960413815,154.7108184,21.512583,55.923255,512
Oman,OMN,2006,4.307714011,158.5429066,21.512583,55.923255,512
Oman,OMN,2007,3.627548475,158.9304142,21.512583,55.923255,512
Oman,OMN,2008,3.028547077,157.2389219,21.512583,55.923255,512
Oman,OMN,2009,2.522887391,152.6592133,21.512583,55.923255,512
Oman,OMN,2010,2.186871577,152.4955167,21.512583,55.923255,512
Oman,OMN,2011,1.831796257,148.4793276,21.512583,55.923255,512
Oman,OMN,2012,1.496733471,142.4999163,21.512583,55.923255,512
Oman,OMN,2013,1.312164155,145.8899034,21.512583,55.923255,512
Oman,OMN,2014,1.153264985,148.2907165,21.512583,55.923255,512
Oman,OMN,2015,1.018143778,152.3071438,21.512583,55.923255,512
Oman,OMN,2016,0.894113258,153.5636209,21.512583,55.923255,512
Oman,OMN,2017,0.766639654,149.3749862,21.512583,55.923255,512
Oman,OMN,2018,0.609250525,135.2062166,21.512583,55.923255,512
Oman,OMN,2019,0.506513832,129.6545226,21.512583,55.923255,512
Pakistan,PAK,1990,203.7673542,47.53256062,30.375321,69.345116,586
Pakistan,PAK,1991,206.611706,48.10758701,30.375321,69.345116,586
Pakistan,PAK,1992,209.2376244,48.62394598,30.375321,69.345116,586
Pakistan,PAK,1993,211.209619,49.41137624,30.375321,69.345116,586
Pakistan,PAK,1994,213.6137698,50.89674691,30.375321,69.345116,586
Pakistan,PAK,1995,216.8506428,53.20383252,30.375321,69.345116,586
Pakistan,PAK,1996,215.4436631,55.08934573,30.375321,69.345116,586
Pakistan,PAK,1997,212.0244073,58.82502609,30.375321,69.345116,586
Pakistan,PAK,1998,205.2790333,63.04142592,30.375321,69.345116,586
Pakistan,PAK,1999,199.70714,68.11013402,30.375321,69.345116,586
Pakistan,PAK,2000,195.8444584,71.34415225,30.375321,69.345116,586
Pakistan,PAK,2001,192.4076909,73.01168677,30.375321,69.345116,586
Pakistan,PAK,2002,188.6186658,73.94623206,30.375321,69.345116,586
Pakistan,PAK,2003,184.2968216,75.97828006,30.375321,69.345116,586
Pakistan,PAK,2004,179.4723379,77.26626933,30.375321,69.345116,586
Pakistan,PAK,2005,174.2653527,79.0261824,30.375321,69.345116,586
Pakistan,PAK,2006,168.6917207,80.79209368,30.375321,69.345116,586
Pakistan,PAK,2007,161.9149758,83.7837077,30.375321,69.345116,586
Pakistan,PAK,2008,156.6085687,86.87177177,30.375321,69.345116,586
Pakistan,PAK,2009,150.4681877,89.04154549,30.375321,69.345116,586
Pakistan,PAK,2010,144.6296004,90.95973204,30.375321,69.345116,586
Pakistan,PAK,2011,138.106722,94.15421859,30.375321,69.345116,586
Pakistan,PAK,2012,131.6788412,98.2563614,30.375321,69.345116,586
Pakistan,PAK,2013,125.7090136,102.9517093,30.375321,69.345116,586
Pakistan,PAK,2014,119.7673921,105.5212804,30.375321,69.345116,586
Pakistan,PAK,2015,114.3114844,106.7887817,30.375321,69.345116,586
Pakistan,PAK,2016,109.921029,106.4842784,30.375321,69.345116,586
Pakistan,PAK,2017,105.4197375,105.8338573,30.375321,69.345116,586
Pakistan,PAK,2018,99.35192299,105.8266598,30.375321,69.345116,586
Pakistan,PAK,2019,92.62799408,108.3554624,30.375321,69.345116,586
Palau,PLW,1990,0.233854357,26.3314129,7.51498,134.58252,585
Palau,PLW,1991,0.202383402,25.00614387,7.51498,134.58252,585
Palau,PLW,1992,0.174260285,23.91549428,7.51498,134.58252,585
Palau,PLW,1993,0.151077118,23.1339252,7.51498,134.58252,585
Palau,PLW,1994,0.133228985,22.63620738,7.51498,134.58252,585
Palau,PLW,1995,0.121476659,22.39377388,7.51498,134.58252,585
Palau,PLW,1996,0.113629955,22.64373874,7.51498,134.58252,585
Palau,PLW,1997,0.106904032,22.92205833,7.51498,134.58252,585
Palau,PLW,1998,0.101578503,23.22580524,7.51498,134.58252,585
Palau,PLW,1999,0.098141187,23.39961597,7.51498,134.58252,585
Palau,PLW,2000,0.095889065,23.48180926,7.51498,134.58252,585
Palau,PLW,2001,0.095520196,23.63675347,7.51498,134.58252,585
Palau,PLW,2002,0.095764812,23.83794554,7.51498,134.58252,585
Palau,PLW,2003,0.096074323,24.05028554,7.51498,134.58252,585
Palau,PLW,2004,0.097252382,24.28599766,7.51498,134.58252,585
Palau,PLW,2005,0.097286162,24.19135183,7.51498,134.58252,585
Palau,PLW,2006,0.094600807,23.36805544,7.51498,134.58252,585
Palau,PLW,2007,0.088793912,21.49423705,7.51498,134.58252,585
Palau,PLW,2008,0.082002689,19.37996309,7.51498,134.58252,585
Palau,PLW,2009,0.076395708,17.57172942,7.51498,134.58252,585
Palau,PLW,2010,0.073899952,16.74156949,7.51498,134.58252,585
Palau,PLW,2011,0.077309202,19.24109588,7.51498,134.58252,585
Palau,PLW,2012,0.084969439,25.20385715,7.51498,134.58252,585
Palau,PLW,2013,0.094209842,32.40906176,7.51498,134.58252,585
Palau,PLW,2014,0.101463298,38.29702327,7.51498,134.58252,585
Palau,PLW,2015,0.10389421,40.40677197,7.51498,134.58252,585
Palau,PLW,2016,0.088258655,32.24256547,7.51498,134.58252,585
Palau,PLW,2017,0.070051073,24.01947242,7.51498,134.58252,585
Palau,PLW,2018,0.064886082,23.82981439,7.51498,134.58252,585
Palau,PLW,2019,0.062324413,23.6770371,7.51498,134.58252,585
Palestine,PSE,1990,72.38968279,67.73046151,31.952162,35.233154,275
Palestine,PSE,1991,64.90129078,74.63782984,31.952162,35.233154,275
Palestine,PSE,1992,57.54311836,80.57422986,31.952162,35.233154,275
Palestine,PSE,1993,50.70518195,85.78469076,31.952162,35.233154,275
Palestine,PSE,1994,44.32502621,89.70059738,31.952162,35.233154,275
Palestine,PSE,1995,38.6520603,92.73652803,31.952162,35.233154,275
Palestine,PSE,1996,33.37775697,95.0856073,31.952162,35.233154,275
Palestine,PSE,1997,28.21032045,96.96072714,31.952162,35.233154,275
Palestine,PSE,1998,23.40884182,97.81370988,31.952162,35.233154,275
Palestine,PSE,1999,19.37697389,98.39839337,31.952162,35.233154,275
Palestine,PSE,2000,16.49621689,99.17039689,31.952162,35.233154,275
Palestine,PSE,2001,14.42253947,100.1639623,31.952162,35.233154,275
Palestine,PSE,2002,12.75675411,101.1558804,31.952162,35.233154,275
Palestine,PSE,2003,11.24225871,101.1234852,31.952162,35.233154,275
Palestine,PSE,2004,9.930223691,100.6985638,31.952162,35.233154,275
Palestine,PSE,2005,8.652609496,99.77687116,31.952162,35.233154,275
Palestine,PSE,2006,7.465151476,99.86427782,31.952162,35.233154,275
Palestine,PSE,2007,6.302643243,99.4116489,31.952162,35.233154,275
Palestine,PSE,2008,5.321718258,99.67082951,31.952162,35.233154,275
Palestine,PSE,2009,4.508021897,99.69296469,31.952162,35.233154,275
Palestine,PSE,2010,3.926614064,99.67506998,31.952162,35.233154,275
Palestine,PSE,2011,3.478712807,98.82947043,31.952162,35.233154,275
Palestine,PSE,2012,2.977273249,93.89926589,31.952162,35.233154,275
Palestine,PSE,2013,2.637332659,91.78904932,31.952162,35.233154,275
Palestine,PSE,2014,2.482831175,95.65196249,31.952162,35.233154,275
Palestine,PSE,2015,2.30423174,98.37196381,31.952162,35.233154,275
Palestine,PSE,2016,2.073794853,95.83350458,31.952162,35.233154,275
Palestine,PSE,2017,1.855413068,93.1023821,31.952162,35.233154,275
Palestine,PSE,2018,1.633869018,91.93554782,31.952162,35.233154,275
Palestine,PSE,2019,1.427560194,91.17547006,31.952162,35.233154,275
Panama,PAN,1990,28.75246038,21.4923027,8.537981,-80.782127,591
Panama,PAN,1991,27.12131931,20.78108161,8.537981,-80.782127,591
Panama,PAN,1992,26.63786724,20.96240787,8.537981,-80.782127,591
Panama,PAN,1993,26.12096717,21.49962608,8.537981,-80.782127,591
Panama,PAN,1994,24.22550853,20.76270816,8.537981,-80.782127,591
Panama,PAN,1995,23.08468306,20.87041644,8.537981,-80.782127,591
Panama,PAN,1996,21.11362965,20.62529071,8.537981,-80.782127,591
Panama,PAN,1997,20.11144168,22.37581445,8.537981,-80.782127,591
Panama,PAN,1998,17.9722518,23.1301438,8.537981,-80.782127,591
Panama,PAN,1999,15.8968009,23.40612451,8.537981,-80.782127,591
Panama,PAN,2000,14.11028265,22.00297601,8.537981,-80.782127,591
Panama,PAN,2001,13.55995274,22.05315954,8.537981,-80.782127,591
Panama,PAN,2002,13.32626279,21.93524273,8.537981,-80.782127,591
Panama,PAN,2003,13.30742577,22.25901194,8.537981,-80.782127,591
Panama,PAN,2004,12.93494727,21.33681126,8.537981,-80.782127,591
Panama,PAN,2005,12.64114458,21.03239673,8.537981,-80.782127,591
Panama,PAN,2006,11.99345617,20.80694358,8.537981,-80.782127,591
Panama,PAN,2007,10.92093713,20.03355306,8.537981,-80.782127,591
Panama,PAN,2008,10.09766215,19.95832519,8.537981,-80.782127,591
Panama,PAN,2009,9.317710842,19.86143835,8.537981,-80.782127,591
Panama,PAN,2010,8.586654809,19.81119667,8.537981,-80.782127,591
Panama,PAN,2011,7.949958095,19.97087716,8.537981,-80.782127,591
Panama,PAN,2012,7.374747308,20.4451932,8.537981,-80.782127,591
Panama,PAN,2013,6.857713267,20.69055085,8.537981,-80.782127,591
Panama,PAN,2014,6.230852779,20.61103765,8.537981,-80.782127,591
Panama,PAN,2015,5.55851692,20.02095932,8.537981,-80.782127,591
Panama,PAN,2016,4.97788612,18.61038331,8.537981,-80.782127,591
Panama,PAN,2017,4.498127667,17.08617405,8.537981,-80.782127,591
Panama,PAN,2018,4.042637119,16.4283485,8.537981,-80.782127,591
Panama,PAN,2019,3.670783514,16.02140535,8.537981,-80.782127,591
Papua New Guinea,PNG,1990,281.9459574,17.04868071,-6.314993,143.95555,598
Papua New Guinea,PNG,1991,280.4955771,17.35858933,-6.314993,143.95555,598
Papua New Guinea,PNG,1992,278.3581175,17.60000793,-6.314993,143.95555,598
Papua New Guinea,PNG,1993,274.8465189,17.71331326,-6.314993,143.95555,598
Papua New Guinea,PNG,1994,271.4678545,17.77083616,-6.314993,143.95555,598
Papua New Guinea,PNG,1995,269.3314299,17.89247839,-6.314993,143.95555,598
Papua New Guinea,PNG,1996,268.0810503,18.23346911,-6.314993,143.95555,598
Papua New Guinea,PNG,1997,266.8793553,18.40398969,-6.314993,143.95555,598
Papua New Guinea,PNG,1998,267.8267333,18.66920468,-6.314993,143.95555,598
Papua New Guinea,PNG,1999,267.8529393,18.69897263,-6.314993,143.95555,598
Papua New Guinea,PNG,2000,267.4377037,18.72863065,-6.314993,143.95555,598
Papua New Guinea,PNG,2001,267.914074,18.67806065,-6.314993,143.95555,598
Papua New Guinea,PNG,2002,268.9630843,18.48971971,-6.314993,143.95555,598
Papua New Guinea,PNG,2003,270.182449,18.2772086,-6.314993,143.95555,598
Papua New Guinea,PNG,2004,272.0957414,18.15051309,-6.314993,143.95555,598
Papua New Guinea,PNG,2005,274.3263294,18.23888845,-6.314993,143.95555,598
Papua New Guinea,PNG,2006,274.277657,18.77880159,-6.314993,143.95555,598
Papua New Guinea,PNG,2007,272.1641557,19.74918293,-6.314993,143.95555,598
Papua New Guinea,PNG,2008,268.4921397,20.86652879,-6.314993,143.95555,598
Papua New Guinea,PNG,2009,264.3943368,21.81925496,-6.314993,143.95555,598
Papua New Guinea,PNG,2010,262.8628172,22.56673061,-6.314993,143.95555,598
Papua New Guinea,PNG,2011,260.1653699,22.90021169,-6.314993,143.95555,598
Papua New Guinea,PNG,2012,256.3859924,23.11495758,-6.314993,143.95555,598
Papua New Guinea,PNG,2013,251.3113326,23.16736716,-6.314993,143.95555,598
Papua New Guinea,PNG,2014,246.8595627,23.27531138,-6.314993,143.95555,598
Papua New Guinea,PNG,2015,243.6291129,23.38223618,-6.314993,143.95555,598
Papua New Guinea,PNG,2016,239.2613136,23.32000963,-6.314993,143.95555,598
Papua New Guinea,PNG,2017,236.1994875,23.33721879,-6.314993,143.95555,598
Papua New Guinea,PNG,2018,233.4896239,23.91881643,-6.314993,143.95555,598
Papua New Guinea,PNG,2019,229.517215,24.67891631,-6.314993,143.95555,598
Paraguay,PRY,1990,69.78538103,16.51125671,-23.442503,-58.443832,600
Paraguay,PRY,1991,64.74508384,15.58173608,-23.442503,-58.443832,600
Paraguay,PRY,1992,66.4590382,16.48187879,-23.442503,-58.443832,600
Paraguay,PRY,1993,66.65878261,16.96809825,-23.442503,-58.443832,600
Paraguay,PRY,1994,65.82756447,17.4885096,-23.442503,-58.443832,600
Paraguay,PRY,1995,65.47323174,18.0474701,-23.442503,-58.443832,600
Paraguay,PRY,1996,64.97662467,18.84325575,-23.442503,-58.443832,600
Paraguay,PRY,1997,60.22259703,18.4763399,-23.442503,-58.443832,600
Paraguay,PRY,1998,58.10187606,19.14311896,-23.442503,-58.443832,600
Paraguay,PRY,1999,56.3555374,19.58137027,-23.442503,-58.443832,600
Paraguay,PRY,2000,53.83499206,19.46544727,-23.442503,-58.443832,600
Paraguay,PRY,2001,50.65558831,18.73766313,-23.442503,-58.443832,600
Paraguay,PRY,2002,48.81268659,18.62182154,-23.442503,-58.443832,600
Paraguay,PRY,2003,48.51535836,18.96180007,-23.442503,-58.443832,600
Paraguay,PRY,2004,49.16022025,19.79882854,-23.442503,-58.443832,600
Paraguay,PRY,2005,47.70835086,19.8755412,-23.442503,-58.443832,600
Paraguay,PRY,2006,46.5616218,20.26087892,-23.442503,-58.443832,600
Paraguay,PRY,2007,43.8707349,20.1266231,-23.442503,-58.443832,600
Paraguay,PRY,2008,42.02356759,20.17836416,-23.442503,-58.443832,600
Paraguay,PRY,2009,41.55517378,21.02634222,-23.442503,-58.443832,600
Paraguay,PRY,2010,40.22529772,21.28237336,-23.442503,-58.443832,600
Paraguay,PRY,2011,37.43955704,20.67782022,-23.442503,-58.443832,600
Paraguay,PRY,2012,34.82421052,20.00254359,-23.442503,-58.443832,600
Paraguay,PRY,2013,33.31823047,19.63697217,-23.442503,-58.443832,600
Paraguay,PRY,2014,30.22517042,18.43872417,-23.442503,-58.443832,600
Paraguay,PRY,2015,28.34314078,18.21597859,-23.442503,-58.443832,600
Paraguay,PRY,2016,27.65082467,19.61062474,-23.442503,-58.443832,600
Paraguay,PRY,2017,25.73592747,20.10716029,-23.442503,-58.443832,600
Paraguay,PRY,2018,23.8463637,20.32488021,-23.442503,-58.443832,600
Paraguay,PRY,2019,22.23704989,20.50188616,-23.442503,-58.443832,600
Peru,PER,1990,62.64738213,42.23076831,-9.189967,-75.015152,604
Peru,PER,1991,54.34168319,37.90412533,-9.189967,-75.015152,604
Peru,PER,1992,53.85348807,39.2884942,-9.189967,-75.015152,604
Peru,PER,1993,50.43328039,38.53460366,-9.189967,-75.015152,604
Peru,PER,1994,47.27505857,37.42041311,-9.189967,-75.015152,604
Peru,PER,1995,45.16667508,37.11234928,-9.189967,-75.015152,604
Peru,PER,1996,40.30831461,34.62728855,-9.189967,-75.015152,604
Peru,PER,1997,37.78319218,33.76061772,-9.189967,-75.015152,604
Peru,PER,1998,35.7593077,33.16137078,-9.189967,-75.015152,604
Peru,PER,1999,32.02128176,30.73043257,-9.189967,-75.015152,604
Peru,PER,2000,30.99043558,30.48024944,-9.189967,-75.015152,604
Peru,PER,2001,28.70951676,28.90222384,-9.189967,-75.015152,604
Peru,PER,2002,27.66848892,28.36954765,-9.189967,-75.015152,604
Peru,PER,2003,27.30633045,28.45519865,-9.189967,-75.015152,604
Peru,PER,2004,25.70279545,27.41173252,-9.189967,-75.015152,604
Peru,PER,2005,24.481185,26.80815961,-9.189967,-75.015152,604
Peru,PER,2006,22.7734933,26.07606319,-9.189967,-75.015152,604
Peru,PER,2007,20.8197786,25.34182077,-9.189967,-75.015152,604
Peru,PER,2008,19.83804963,25.75616136,-9.189967,-75.015152,604
Peru,PER,2009,20.7997127,29.08364497,-9.189967,-75.015152,604
Peru,PER,2010,20.07051176,30.2453793,-9.189967,-75.015152,604
Peru,PER,2011,18.56203433,30.30575215,-9.189967,-75.015152,604
Peru,PER,2012,16.93761068,30.28339865,-9.189967,-75.015152,604
Peru,PER,2013,15.27204359,29.95679699,-9.189967,-75.015152,604
Peru,PER,2014,13.35039895,28.88232243,-9.189967,-75.015152,604
Peru,PER,2015,11.70826368,28.02414686,-9.189967,-75.015152,604
Peru,PER,2016,10.40755137,27.78135595,-9.189967,-75.015152,604
Peru,PER,2017,9.242381984,27.50971338,-9.189967,-75.015152,604
Peru,PER,2018,8.295267422,27.55054527,-9.189967,-75.015152,604
Peru,PER,2019,7.496967948,27.65739394,-9.189967,-75.015152,604
Philippines,PHL,1990,97.46503914,36.34862131,12.879721,121.774017,608
Philippines,PHL,1991,89.37857122,35.06592187,12.879721,121.774017,608
Philippines,PHL,1992,85.80553887,35.35267206,12.879721,121.774017,608
Philippines,PHL,1993,83.08353593,36.01970933,12.879721,121.774017,608
Philippines,PHL,1994,81.27870279,36.9065295,12.879721,121.774017,608
Philippines,PHL,1995,79.8115438,37.87210908,12.879721,121.774017,608
Philippines,PHL,1996,79.16104677,39.33292229,12.879721,121.774017,608
Philippines,PHL,1997,77.22785648,40.3438846,12.879721,121.774017,608
Philippines,PHL,1998,76.61302468,41.98815753,12.879721,121.774017,608
Philippines,PHL,1999,76.79969902,43.88662186,12.879721,121.774017,608
Philippines,PHL,2000,79.04030486,46.4639856,12.879721,121.774017,608
Philippines,PHL,2001,82.33050383,49.09266556,12.879721,121.774017,608
Philippines,PHL,2002,85.68639027,51.0797888,12.879721,121.774017,608
Philippines,PHL,2003,85.83567199,50.92588889,12.879721,121.774017,608
Philippines,PHL,2004,86.51483388,50.80342222,12.879721,121.774017,608
Philippines,PHL,2005,89.57360544,51.72431539,12.879721,121.774017,608
Philippines,PHL,2006,91.04890648,51.16227533,12.879721,121.774017,608
Philippines,PHL,2007,91.93371769,49.41921935,12.879721,121.774017,608
Philippines,PHL,2008,94.78445695,48.70810258,12.879721,121.774017,608
Philippines,PHL,2009,96.40770502,47.70051343,12.879721,121.774017,608
Philippines,PHL,2010,96.34695942,46.60116863,12.879721,121.774017,608
Philippines,PHL,2011,94.94778165,45.81060961,12.879721,121.774017,608
Philippines,PHL,2012,91.4776936,45.46571457,12.879721,121.774017,608
Philippines,PHL,2013,85.7353668,44.99031765,12.879721,121.774017,608
Philippines,PHL,2014,79.86719561,44.57172955,12.879721,121.774017,608
Philippines,PHL,2015,76.03688203,44.65422155,12.879721,121.774017,608
Philippines,PHL,2016,72.42308239,43.93006661,12.879721,121.774017,608
Philippines,PHL,2017,68.83301898,43.44443094,12.879721,121.774017,608
Philippines,PHL,2018,64.84510026,43.5831803,12.879721,121.774017,608
Philippines,PHL,2019,60.88400766,44.12201326,12.879721,121.774017,608
Poland,POL,1990,32.87956416,91.95772434,51.919438,19.145136,616
Poland,POL,1991,31.88813961,96.09148818,51.919438,19.145136,616
Poland,POL,1992,29.23253563,93.95136197,51.919438,19.145136,616
Poland,POL,1993,26.50506906,90.58995398,51.919438,19.145136,616
Poland,POL,1994,24.60441083,89.16446379,51.919438,19.145136,616
Poland,POL,1995,22.95547157,88.34185964,51.919438,19.145136,616
Poland,POL,1996,20.96256461,84.5560551,51.919438,19.145136,616
Poland,POL,1997,19.34353954,81.61162062,51.919438,19.145136,616
Poland,POL,1998,17.51693548,77.23816818,51.919438,19.145136,616
Poland,POL,1999,16.27820721,75.21675578,51.919438,19.145136,616
Poland,POL,2000,14.48236606,69.61538208,51.919438,19.145136,616
Poland,POL,2001,13.27024651,66.58743985,51.919438,19.145136,616
Poland,POL,2002,12.26028528,64.07223182,51.919438,19.145136,616
Poland,POL,2003,11.47737846,62.4021216,51.919438,19.145136,616
Poland,POL,2004,10.80955417,61.20561757,51.919438,19.145136,616
Poland,POL,2005,10.13564865,59.81102154,51.919438,19.145136,616
Poland,POL,2006,9.535000713,58.98918459,51.919438,19.145136,616
Poland,POL,2007,8.99342249,58.57277996,51.919438,19.145136,616
Poland,POL,2008,8.390349012,57.44781279,51.919438,19.145136,616
Poland,POL,2009,7.817601281,56.08667953,51.919438,19.145136,616
Poland,POL,2010,7.08396263,53.15933921,51.919438,19.145136,616
Poland,POL,2011,6.554921158,50.81892068,51.919438,19.145136,616
Poland,POL,2012,6.198046333,48.84718151,51.919438,19.145136,616
Poland,POL,2013,5.752817209,45.71750851,51.919438,19.145136,616
Poland,POL,2014,5.254232966,42.2758674,51.919438,19.145136,616
Poland,POL,2015,5.017492219,41.60720906,51.919438,19.145136,616
Poland,POL,2016,4.644526875,40.33791245,51.919438,19.145136,616
Poland,POL,2017,4.386116772,39.99098562,51.919438,19.145136,616
Poland,POL,2018,4.15003599,39.99763065,51.919438,19.145136,616
Poland,POL,2019,3.897970928,39.63314863,51.919438,19.145136,616
Portugal,PRT,1990,4.51958699,30.55968581,39.399872,-8.224454,620
Portugal,PRT,1991,4.065292965,30.11914475,39.399872,-8.224454,620
Portugal,PRT,1992,3.553632771,28.91566314,39.399872,-8.224454,620
Portugal,PRT,1993,3.186329862,28.54094045,39.399872,-8.224454,620
Portugal,PRT,1994,2.735280475,26.62120969,39.399872,-8.224454,620
Portugal,PRT,1995,2.461384783,26.32719199,39.399872,-8.224454,620
Portugal,PRT,1996,2.226810736,26.10991507,39.399872,-8.224454,620
Portugal,PRT,1997,1.98813976,25.75785419,39.399872,-8.224454,620
Portugal,PRT,1998,1.797061985,25.54461157,39.399872,-8.224454,620
Portugal,PRT,1999,1.630890255,25.59654281,39.399872,-8.224454,620
Portugal,PRT,2000,1.428313487,24.88142498,39.399872,-8.224454,620
Portugal,PRT,2001,1.244433287,23.79936707,39.399872,-8.224454,620
Portugal,PRT,2002,1.091691342,22.99653325,39.399872,-8.224454,620
Portugal,PRT,2003,0.950175504,21.98491131,39.399872,-8.224454,620
Portugal,PRT,2004,0.79455486,20.42633433,39.399872,-8.224454,620
Portugal,PRT,2005,0.685422923,19.46821645,39.399872,-8.224454,620
Portugal,PRT,2006,0.583582828,18.20823708,39.399872,-8.224454,620
Portugal,PRT,2007,0.50503165,16.9147655,39.399872,-8.224454,620
Portugal,PRT,2008,0.435594914,15.69442128,39.399872,-8.224454,620
Portugal,PRT,2009,0.378737994,14.79023832,39.399872,-8.224454,620
Portugal,PRT,2010,0.32877739,13.81035573,39.399872,-8.224454,620
Portugal,PRT,2011,0.288363661,12.87187832,39.399872,-8.224454,620
Portugal,PRT,2012,0.256402154,12.2403776,39.399872,-8.224454,620
Portugal,PRT,2013,0.227740185,11.54227078,39.399872,-8.224454,620
Portugal,PRT,2014,0.202578638,10.78853057,39.399872,-8.224454,620
Portugal,PRT,2015,0.181259908,9.996282846,39.399872,-8.224454,620
Portugal,PRT,2016,0.164803594,9.494159264,39.399872,-8.224454,620
Portugal,PRT,2017,0.150432986,9.153795297,39.399872,-8.224454,620
Portugal,PRT,2018,0.136342391,8.933638602,39.399872,-8.224454,620
Portugal,PRT,2019,0.123537924,8.734907589,39.399872,-8.224454,620
Puerto Rico,PRI,1990,0.069026302,13.44330318,18.220833,-66.590149,630
Puerto Rico,PRI,1991,0.062688405,13.16587943,18.220833,-66.590149,630
Puerto Rico,PRI,1992,0.057997925,13.13990522,18.220833,-66.590149,630
Puerto Rico,PRI,1993,0.05417259,13.0914032,18.220833,-66.590149,630
Puerto Rico,PRI,1994,0.049444624,12.73606417,18.220833,-66.590149,630
Puerto Rico,PRI,1995,0.04756618,13.03395865,18.220833,-66.590149,630
Puerto Rico,PRI,1996,0.044182035,12.59221491,18.220833,-66.590149,630
Puerto Rico,PRI,1997,0.039577012,11.47926695,18.220833,-66.590149,630
Puerto Rico,PRI,1998,0.038748835,11.28042603,18.220833,-66.590149,630
Puerto Rico,PRI,1999,0.03473502,10.08118226,18.220833,-66.590149,630
Puerto Rico,PRI,2000,0.032004093,9.310708331,18.220833,-66.590149,630
Puerto Rico,PRI,2001,0.030172529,9.171605883,18.220833,-66.590149,630
Puerto Rico,PRI,2002,0.026590756,8.248313756,18.220833,-66.590149,630
Puerto Rico,PRI,2003,0.024712483,7.766721829,18.220833,-66.590149,630
Puerto Rico,PRI,2004,0.023072452,6.976837843,18.220833,-66.590149,630
Puerto Rico,PRI,2005,0.021676756,6.56724061,18.220833,-66.590149,630
Puerto Rico,PRI,2006,0.019983636,6.19535958,18.220833,-66.590149,630
Puerto Rico,PRI,2007,0.019031017,6.107479517,18.220833,-66.590149,630
Puerto Rico,PRI,2008,0.018127213,6.044912724,18.220833,-66.590149,630
Puerto Rico,PRI,2009,0.017458221,6.054728167,18.220833,-66.590149,630
Puerto Rico,PRI,2010,0.015839056,5.740488675,18.220833,-66.590149,630
Puerto Rico,PRI,2011,0.015743437,6.102388967,18.220833,-66.590149,630
Puerto Rico,PRI,2012,0.013984286,5.786281998,18.220833,-66.590149,630
Puerto Rico,PRI,2013,0.013260536,5.873531762,18.220833,-66.590149,630
Puerto Rico,PRI,2014,0.012179416,5.729369846,18.220833,-66.590149,630
Puerto Rico,PRI,2015,0.01087207,5.443509345,18.220833,-66.590149,630
Puerto Rico,PRI,2016,0.010593527,5.621216326,18.220833,-66.590149,630
Puerto Rico,PRI,2017,0.010194623,5.672278738,18.220833,-66.590149,630
Puerto Rico,PRI,2018,0.010044632,5.853909088,18.220833,-66.590149,630
Puerto Rico,PRI,2019,0.009810973,5.944765712,18.220833,-66.590149,630
Qatar,QAT,1990,0.742992735,196.7794319,25.354826,51.183884,634
Qatar,QAT,1991,0.647882445,202.7931408,25.354826,51.183884,634
Qatar,QAT,1992,0.556125969,207.3664002,25.354826,51.183884,634
Qatar,QAT,1993,0.470703711,209.6075501,25.354826,51.183884,634
Qatar,QAT,1994,0.334697463,177.6620927,25.354826,51.183884,634
Qatar,QAT,1995,0.249379685,157.8209645,25.354826,51.183884,634
Qatar,QAT,1996,0.245524865,186.790176,25.354826,51.183884,634
Qatar,QAT,1997,0.224984514,204.1739447,25.354826,51.183884,634
Qatar,QAT,1998,0.192771697,207.0597118,25.354826,51.183884,634
Qatar,QAT,1999,0.1604704,201.8007805,25.354826,51.183884,634
Qatar,QAT,2000,0.128303519,186.9263618,25.354826,51.183884,634
Qatar,QAT,2001,0.107808549,181.386661,25.354826,51.183884,634
Qatar,QAT,2002,0.094511442,184.7413001,25.354826,51.183884,634
Qatar,QAT,2003,0.080485932,183.4951,25.354826,51.183884,634
Qatar,QAT,2004,0.066673349,175.4083323,25.354826,51.183884,634
Qatar,QAT,2005,0.058068953,175.0869723,25.354826,51.183884,634
Qatar,QAT,2006,0.053503844,182.3706688,25.354826,51.183884,634
Qatar,QAT,2007,0.047742522,184.4992129,25.354826,51.183884,634
Qatar,QAT,2008,0.040695674,178.4976475,25.354826,51.183884,634
Qatar,QAT,2009,0.034898145,172.3862818,25.354826,51.183884,634
Qatar,QAT,2010,0.029420277,164.2860449,25.354826,51.183884,634
Qatar,QAT,2011,0.024475355,156.4017236,25.354826,51.183884,634
Qatar,QAT,2012,0.020451832,150.7589787,25.354826,51.183884,634
Qatar,QAT,2013,0.01744001,147.8884375,25.354826,51.183884,634
Qatar,QAT,2014,0.015256448,148.317841,25.354826,51.183884,634
Qatar,QAT,2015,0.013944602,154.5042019,25.354826,51.183884,634
Qatar,QAT,2016,0.012491116,149.6848918,25.354826,51.183884,634
Qatar,QAT,2017,0.011289528,144.9054049,25.354826,51.183884,634
Qatar,QAT,2018,0.009816714,137.6218178,25.354826,51.183884,634
Qatar,QAT,2019,0.008503593,132.7259511,25.354826,51.183884,634
Romania,ROU,1990,53.48556422,77.23977235,45.943161,24.96676,642
Romania,ROU,1991,50.95250356,77.27698034,45.943161,24.96676,642
Romania,ROU,1992,50.52768442,80.20854577,45.943161,24.96676,642
Romania,ROU,1993,48.36688437,80.52420306,45.943161,24.96676,642
Romania,ROU,1994,46.41546294,80.64800753,45.943161,24.96676,642
Romania,ROU,1995,45.3248596,82.59959808,45.943161,24.96676,642
Romania,ROU,1996,44.81275723,84.74691955,45.943161,24.96676,642
Romania,ROU,1997,42.27758507,83.22123551,45.943161,24.96676,642
Romania,ROU,1998,38.65815868,78.39804933,45.943161,24.96676,642
Romania,ROU,1999,34.92948947,73.39669307,45.943161,24.96676,642
Romania,ROU,2000,31.64723061,69.12246989,45.943161,24.96676,642
Romania,ROU,2001,29.84602774,68.99842764,45.943161,24.96676,642
Romania,ROU,2002,28.10837657,69.533499,45.943161,24.96676,642
Romania,ROU,2003,25.67053434,67.81243187,45.943161,24.96676,642
Romania,ROU,2004,22.78908845,64.32374266,45.943161,24.96676,642
Romania,ROU,2005,20.76707691,62.17897976,45.943161,24.96676,642
Romania,ROU,2006,18.33137272,59.60779528,45.943161,24.96676,642
Romania,ROU,2007,15.9418195,56.85170356,45.943161,24.96676,642
Romania,ROU,2008,14.28191317,56.30858287,45.943161,24.96676,642
Romania,ROU,2009,12.95346072,55.60579351,45.943161,24.96676,642
Romania,ROU,2010,11.76462758,54.11386895,45.943161,24.96676,642
Romania,ROU,2011,10.38695442,49.73656574,45.943161,24.96676,642
Romania,ROU,2012,9.743989235,47.97357881,45.943161,24.96676,642
Romania,ROU,2013,8.801852189,43.97021965,45.943161,24.96676,642
Romania,ROU,2014,8.517154121,43.09336144,45.943161,24.96676,642
Romania,ROU,2015,7.968648146,41.17936874,45.943161,24.96676,642
Romania,ROU,2016,7.50069306,40.01604159,45.943161,24.96676,642
Romania,ROU,2017,7.110575857,39.36003999,45.943161,24.96676,642
Romania,ROU,2018,6.751389379,39.07311043,45.943161,24.96676,642
Romania,ROU,2019,6.396273712,38.9313303,45.943161,24.96676,642
Russia,RUS,1990,8.389465477,73.64609021,61.52401,105.318756,643
Russia,RUS,1991,7.905954776,72.29370572,61.52401,105.318756,643
Russia,RUS,1992,7.833992023,75.18082654,61.52401,105.318756,643
Russia,RUS,1993,8.543171732,86.55976566,61.52401,105.318756,643
Russia,RUS,1994,8.744700372,92.43693949,61.52401,105.318756,643
Russia,RUS,1995,8.013090368,86.64963078,61.52401,105.318756,643
Russia,RUS,1996,7.380961699,79.98195348,61.52401,105.318756,643
Russia,RUS,1997,6.887432079,74.57793567,61.52401,105.318756,643
Russia,RUS,1998,6.592980947,71.9966965,61.52401,105.318756,643
Russia,RUS,1999,6.833145283,75.82172816,61.52401,105.318756,643
Russia,RUS,2000,6.80030389,77.14741196,61.52401,105.318756,643
Russia,RUS,2001,6.49519265,76.40635706,61.52401,105.318756,643
Russia,RUS,2002,6.2094873,76.21963685,61.52401,105.318756,643
Russia,RUS,2003,5.77936703,75.31137632,61.52401,105.318756,643
Russia,RUS,2004,5.080858916,70.93163317,61.52401,105.318756,643
Russia,RUS,2005,4.739891243,71.60589419,61.52401,105.318756,643
Russia,RUS,2006,3.928491145,65.43086805,61.52401,105.318756,643
Russia,RUS,2007,3.340969833,62.68119432,61.52401,105.318756,643
Russia,RUS,2008,2.966640491,63.50618935,61.52401,105.318756,643
Russia,RUS,2009,2.527591503,60.96997596,61.52401,105.318756,643
Russia,RUS,2010,2.303422962,60.91329004,61.52401,105.318756,643
Russia,RUS,2011,1.995224231,55.27750661,61.52401,105.318756,643
Russia,RUS,2012,1.793242741,51.16710154,61.52401,105.318756,643
Russia,RUS,2013,1.629266294,47.03442914,61.52401,105.318756,643
Russia,RUS,2014,1.535462597,44.40920845,61.52401,105.318756,643
Russia,RUS,2015,1.407677964,41.03967431,61.52401,105.318756,643
Russia,RUS,2016,1.284169177,36.94694261,61.52401,105.318756,643
Russia,RUS,2017,1.134543445,32.4875928,61.52401,105.318756,643
Russia,RUS,2018,1.083234838,31.96043006,61.52401,105.318756,643
Russia,RUS,2019,1.052939981,32.35393235,61.52401,105.318756,643
Rwanda,RWA,1990,285.1723398,28.14530989,-1.940278,29.873888,646
Rwanda,RWA,1991,288.3067204,28.51487034,-1.940278,29.873888,646
Rwanda,RWA,1992,297.2222431,29.15966792,-1.940278,29.873888,646
Rwanda,RWA,1993,305.2506618,29.55126065,-1.940278,29.873888,646
Rwanda,RWA,1994,300.93066,29.16216765,-1.940278,29.873888,646
Rwanda,RWA,1995,294.0688212,28.93251004,-1.940278,29.873888,646
Rwanda,RWA,1996,285.5153984,28.56205474,-1.940278,29.873888,646
Rwanda,RWA,1997,278.8953453,28.75201053,-1.940278,29.873888,646
Rwanda,RWA,1998,272.3806391,28.60702222,-1.940278,29.873888,646
Rwanda,RWA,1999,258.3061858,28.20886065,-1.940278,29.873888,646
Rwanda,RWA,2000,243.6242149,26.94780907,-1.940278,29.873888,646
Rwanda,RWA,2001,228.6465947,25.93101776,-1.940278,29.873888,646
Rwanda,RWA,2002,219.285644,25.27490848,-1.940278,29.873888,646
Rwanda,RWA,2003,209.0121598,24.78919264,-1.940278,29.873888,646
Rwanda,RWA,2004,200.6301122,24.93337119,-1.940278,29.873888,646
Rwanda,RWA,2005,189.5804722,24.88719152,-1.940278,29.873888,646
Rwanda,RWA,2006,178.9649598,25.13043009,-1.940278,29.873888,646
Rwanda,RWA,2007,171.1269141,24.77484583,-1.940278,29.873888,646
Rwanda,RWA,2008,164.4556207,24.54707545,-1.940278,29.873888,646
Rwanda,RWA,2009,154.9105471,24.22622368,-1.940278,29.873888,646
Rwanda,RWA,2010,150.1881558,25.01578134,-1.940278,29.873888,646
Rwanda,RWA,2011,145.2773594,26.04104045,-1.940278,29.873888,646
Rwanda,RWA,2012,141.9304887,27.40742511,-1.940278,29.873888,646
Rwanda,RWA,2013,136.101038,28.39934805,-1.940278,29.873888,646
Rwanda,RWA,2014,133.4907275,29.38463069,-1.940278,29.873888,646
Rwanda,RWA,2015,131.163388,29.93360489,-1.940278,29.873888,646
Rwanda,RWA,2016,128.6095545,29.34780623,-1.940278,29.873888,646
Rwanda,RWA,2017,126.3998632,29.22628678,-1.940278,29.873888,646
Rwanda,RWA,2018,125.0799772,30.71179205,-1.940278,29.873888,646
Rwanda,RWA,2019,122.6652152,32.41149411,-1.940278,29.873888,646
Saint Kitts and Nevis,KNA,1990,27.19973237,34.47757966,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1991,21.33259112,29.9958282,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1992,19.40004562,29.54916094,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1993,17.41462146,28.73884549,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1994,16.32028676,29.12305852,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1995,15.36786933,29.68520785,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1996,13.85419056,29.06776405,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1997,12.39041145,28.35221802,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1998,11.08859415,27.54383843,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,1999,9.880271174,26.62154249,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2000,8.786295574,25.49013249,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2001,7.840805383,24.40142913,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2002,6.964805033,22.83306247,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2003,6.15000788,21.11876186,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2004,5.521487823,19.84428993,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2005,4.951509302,18.96551804,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2006,4.499940183,18.70241685,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2007,4.055027887,18.44692332,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2008,3.503617009,17.25965929,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2009,3.178886183,17.0973255,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2010,2.908379418,17.01661056,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2011,2.679615646,17.03725465,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2012,2.478046347,17.18023226,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2013,2.311260573,17.47044981,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2014,2.164744612,17.77394213,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2015,2.028911429,17.99562411,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2016,1.866452928,17.75538819,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2017,1.729848061,17.62226228,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2018,1.628551281,17.92779153,17.357822,-62.782998,659
Saint Kitts and Nevis,KNA,2019,1.581175852,19.10320024,17.357822,-62.782998,659
Saint Lucia,LCA,1990,58.01849134,45.09294948,13.909444,-60.978893,662
Saint Lucia,LCA,1991,52.28748659,46.99084475,13.909444,-60.978893,662
Saint Lucia,LCA,1992,46.99849519,48.84841361,13.909444,-60.978893,662
Saint Lucia,LCA,1993,41.63684562,50.01997309,13.909444,-60.978893,662
Saint Lucia,LCA,1994,36.31440581,50.12258583,13.909444,-60.978893,662
Saint Lucia,LCA,1995,31.99946861,50.2367637,13.909444,-60.978893,662
Saint Lucia,LCA,1996,27.76679316,49.41193234,13.909444,-60.978893,662
Saint Lucia,LCA,1997,24.02075327,48.45108845,13.909444,-60.978893,662
Saint Lucia,LCA,1998,20.914089,47.37151093,13.909444,-60.978893,662
Saint Lucia,LCA,1999,18.47358988,46.65042653,13.909444,-60.978893,662
Saint Lucia,LCA,2000,16.28947535,45.2748824,13.909444,-60.978893,662
Saint Lucia,LCA,2001,14.79659705,45.02838211,13.909444,-60.978893,662
Saint Lucia,LCA,2002,13.37884933,44.09204098,13.909444,-60.978893,662
Saint Lucia,LCA,2003,12.04826277,42.96879723,13.909444,-60.978893,662
Saint Lucia,LCA,2004,10.77096676,41.46521028,13.909444,-60.978893,662
Saint Lucia,LCA,2005,9.492247849,39.87051771,13.909444,-60.978893,662
Saint Lucia,LCA,2006,8.1645217,38.15385524,13.909444,-60.978893,662
Saint Lucia,LCA,2007,6.772925773,36.24006708,13.909444,-60.978893,662
Saint Lucia,LCA,2008,5.753350248,35.38574591,13.909444,-60.978893,662
Saint Lucia,LCA,2009,4.897931199,34.59996234,13.909444,-60.978893,662
Saint Lucia,LCA,2010,4.164804397,33.28137078,13.909444,-60.978893,662
Saint Lucia,LCA,2011,3.676357904,32.97608538,13.909444,-60.978893,662
Saint Lucia,LCA,2012,3.282950521,33.46135566,13.909444,-60.978893,662
Saint Lucia,LCA,2013,3.064306228,35.5369008,13.909444,-60.978893,662
Saint Lucia,LCA,2014,2.827713017,36.73826955,13.909444,-60.978893,662
Saint Lucia,LCA,2015,2.641884998,37.47435283,13.909444,-60.978893,662
Saint Lucia,LCA,2016,2.659974943,39.31125194,13.909444,-60.978893,662
Saint Lucia,LCA,2017,2.536604722,38.68929449,13.909444,-60.978893,662
Saint Lucia,LCA,2018,2.406485682,39.08760414,13.909444,-60.978893,662
Saint Lucia,LCA,2019,2.267428875,39.72040808,13.909444,-60.978893,662
Saint Vincent and the Grenadines,VCT,1990,50.68770852,40.52474107,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1991,46.42412939,42.85420383,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1992,42.46294669,45.18426135,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1993,38.48928566,47.16274648,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1994,34.59182322,48.5723263,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1995,29.77934266,48.25557663,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1996,26.42913717,49.29567803,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1997,23.23815918,50.03061287,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1998,20.67935151,51.25606624,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,1999,18.17353705,51.51139612,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2000,16.02250459,51.16614545,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2001,13.75614642,48.90426987,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2002,12.01959602,47.90112755,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2003,10.45800446,46.70189379,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2004,9.169377958,45.6556965,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2005,8.084919079,44.28967156,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2006,7.154571898,43.02512662,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2007,6.455872739,42.42714088,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2008,6.086514704,43.4845838,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2009,5.765112964,44.41507342,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2010,5.498733836,45.31223277,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2011,5.348635154,47.0211237,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2012,5.154256654,48.73693604,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2013,4.945481368,50.18329262,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2014,4.792927506,51.7202335,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2015,4.530984285,51.6775112,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2016,4.247906359,50.02694325,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2017,4.016738713,48.85383564,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2018,3.773902652,48.79995274,12.984305,-61.287228,670
Saint Vincent and the Grenadines,VCT,2019,3.530240083,49.33771098,12.984305,-61.287228,670
Samoa,WSM,1990,159.5122495,30.18919641,-13.759029,-172.104629,882
Samoa,WSM,1991,156.9454262,30.63580891,-13.759029,-172.104629,882
Samoa,WSM,1992,154.6708781,31.25754021,-13.759029,-172.104629,882
Samoa,WSM,1993,152.0168081,31.61560968,-13.759029,-172.104629,882
Samoa,WSM,1994,149.8346899,31.11941153,-13.759029,-172.104629,882
Samoa,WSM,1995,148.1975671,30.59557643,-13.759029,-172.104629,882
Samoa,WSM,1996,146.2409357,30.19969092,-13.759029,-172.104629,882
Samoa,WSM,1997,143.8439297,30.66457406,-13.759029,-172.104629,882
Samoa,WSM,1998,141.3696699,30.63293052,-13.759029,-172.104629,882
Samoa,WSM,1999,140.2429718,30.56143242,-13.759029,-172.104629,882
Samoa,WSM,2000,138.9264548,30.02833583,-13.759029,-172.104629,882
Samoa,WSM,2001,137.8089875,29.6861653,-13.759029,-172.104629,882
Samoa,WSM,2002,136.9552981,29.67174512,-13.759029,-172.104629,882
Samoa,WSM,2003,136.9618429,29.70670093,-13.759029,-172.104629,882
Samoa,WSM,2004,136.6480011,29.75011632,-13.759029,-172.104629,882
Samoa,WSM,2005,136.1163558,29.63913221,-13.759029,-172.104629,882
Samoa,WSM,2006,135.5571807,29.70913098,-13.759029,-172.104629,882
Samoa,WSM,2007,134.6589832,29.22578327,-13.759029,-172.104629,882
Samoa,WSM,2008,133.7519649,28.79542621,-13.759029,-172.104629,882
Samoa,WSM,2009,133.0212895,28.25321624,-13.759029,-172.104629,882
Samoa,WSM,2010,132.114075,27.91728975,-13.759029,-172.104629,882
Samoa,WSM,2011,131.1238222,27.74023127,-13.759029,-172.104629,882
Samoa,WSM,2012,129.2462291,27.72515558,-13.759029,-172.104629,882
Samoa,WSM,2013,126.7537112,28.06213024,-13.759029,-172.104629,882
Samoa,WSM,2014,123.9834768,28.11654403,-13.759029,-172.104629,882
Samoa,WSM,2015,121.0240715,28.33225962,-13.759029,-172.104629,882
Samoa,WSM,2016,116.4277006,28.54425723,-13.759029,-172.104629,882
Samoa,WSM,2017,110.995249,28.78914655,-13.759029,-172.104629,882
Samoa,WSM,2018,106.0308425,29.84977565,-13.759029,-172.104629,882
Samoa,WSM,2019,100.9005555,30.52446862,-13.759029,-172.104629,882
San Marino,SMR,1990,0.153997241,17.1342446,43.94236,12.457777,674
San Marino,SMR,1991,0.140295928,16.51939788,43.94236,12.457777,674
San Marino,SMR,1992,0.127951205,15.90178674,43.94236,12.457777,674
San Marino,SMR,1993,0.116293301,15.32994991,43.94236,12.457777,674
San Marino,SMR,1994,0.106949118,14.88824075,43.94236,12.457777,674
San Marino,SMR,1995,0.097161149,14.2597168,43.94236,12.457777,674
San Marino,SMR,1996,0.088275487,13.67822706,43.94236,12.457777,674
San Marino,SMR,1997,0.080482014,13.19326145,43.94236,12.457777,674
San Marino,SMR,1998,0.073898391,12.73851886,43.94236,12.457777,674
San Marino,SMR,1999,0.067723005,12.12572311,43.94236,12.457777,674
San Marino,SMR,2000,0.062753998,11.63600732,43.94236,12.457777,674
San Marino,SMR,2001,0.058478809,11.15597323,43.94236,12.457777,674
San Marino,SMR,2002,0.054671039,11.07767191,43.94236,12.457777,674
San Marino,SMR,2003,0.051501994,10.82013876,43.94236,12.457777,674
San Marino,SMR,2004,0.048810553,10.82725131,43.94236,12.457777,674
San Marino,SMR,2005,0.045978638,10.45558278,43.94236,12.457777,674
San Marino,SMR,2006,0.042462851,10.08853667,43.94236,12.457777,674
San Marino,SMR,2007,0.038671409,9.437816087,43.94236,12.457777,674
San Marino,SMR,2008,0.035153657,8.915905344,43.94236,12.457777,674
San Marino,SMR,2009,0.032410449,8.441627436,43.94236,12.457777,674
San Marino,SMR,2010,0.030528666,8.328339932,43.94236,12.457777,674
San Marino,SMR,2011,0.029431483,8.470175278,43.94236,12.457777,674
San Marino,SMR,2012,0.028615963,8.846322396,43.94236,12.457777,674
San Marino,SMR,2013,0.027935723,9.204265217,43.94236,12.457777,674
San Marino,SMR,2014,0.027315219,9.490075866,43.94236,12.457777,674
San Marino,SMR,2015,0.026583683,9.465664002,43.94236,12.457777,674
San Marino,SMR,2016,0.025477502,9.302092485,43.94236,12.457777,674
San Marino,SMR,2017,0.024296789,9.082025737,43.94236,12.457777,674
San Marino,SMR,2018,0.023275937,9.215877346,43.94236,12.457777,674
San Marino,SMR,2019,0.022331945,9.237197641,43.94236,12.457777,674
Sao Tome and Principe,STP,1990,197.5439087,23.29845708,0.18636,6.613081,678
Sao Tome and Principe,STP,1991,197.1784774,23.31850082,0.18636,6.613081,678
Sao Tome and Principe,STP,1992,197.1987423,23.46934612,0.18636,6.613081,678
Sao Tome and Principe,STP,1993,194.1529999,23.24332175,0.18636,6.613081,678
Sao Tome and Principe,STP,1994,193.4373836,23.39870446,0.18636,6.613081,678
Sao Tome and Principe,STP,1995,193.6326224,23.85751885,0.18636,6.613081,678
Sao Tome and Principe,STP,1996,194.9583594,24.88641728,0.18636,6.613081,678
Sao Tome and Principe,STP,1997,194.7569673,26.41156317,0.18636,6.613081,678
Sao Tome and Principe,STP,1998,193.8543358,28.33691296,0.18636,6.613081,678
Sao Tome and Principe,STP,1999,190.3127587,30.14268526,0.18636,6.613081,678
Sao Tome and Principe,STP,2000,182.424615,30.41599481,0.18636,6.613081,678
Sao Tome and Principe,STP,2001,177.8253696,31.53855368,0.18636,6.613081,678
Sao Tome and Principe,STP,2002,175.3287149,33.32948253,0.18636,6.613081,678
Sao Tome and Principe,STP,2003,166.6266131,34.32939831,0.18636,6.613081,678
Sao Tome and Principe,STP,2004,165.4771154,36.75034446,0.18636,6.613081,678
Sao Tome and Principe,STP,2005,155.0396213,37.01796367,0.18636,6.613081,678
Sao Tome and Principe,STP,2006,153.897475,38.95383246,0.18636,6.613081,678
Sao Tome and Principe,STP,2007,149.8084197,39.38865772,0.18636,6.613081,678
Sao Tome and Principe,STP,2008,143.7340449,38.73574723,0.18636,6.613081,678
Sao Tome and Principe,STP,2009,140.2911683,39.51409249,0.18636,6.613081,678
Sao Tome and Principe,STP,2010,137.162004,40.97164385,0.18636,6.613081,678
Sao Tome and Principe,STP,2011,130.019663,43.02519522,0.18636,6.613081,678
Sao Tome and Principe,STP,2012,123.8120439,46.69422466,0.18636,6.613081,678
Sao Tome and Principe,STP,2013,118.8351074,51.67108198,0.18636,6.613081,678
Sao Tome and Principe,STP,2014,115.3095113,56.34923059,0.18636,6.613081,678
Sao Tome and Principe,STP,2015,110.3337611,57.84363056,0.18636,6.613081,678
Sao Tome and Principe,STP,2016,106.2805639,54.81466138,0.18636,6.613081,678
Sao Tome and Principe,STP,2017,102.5213803,52.14051935,0.18636,6.613081,678
Sao Tome and Principe,STP,2018,97.24730911,54.03666246,0.18636,6.613081,678
Sao Tome and Principe,STP,2019,90.81726467,57.18679159,0.18636,6.613081,678
Saudi Arabia,SAU,1990,76.8869317,81.14392805,23.885942,45.079162,682
Saudi Arabia,SAU,1991,66.21434874,89.90527972,23.885942,45.079162,682
Saudi Arabia,SAU,1992,55.84716848,97.86346712,23.885942,45.079162,682
Saudi Arabia,SAU,1993,46.42585172,105.2205142,23.885942,45.079162,682
Saudi Arabia,SAU,1994,38.32620825,112.0928407,23.885942,45.079162,682
Saudi Arabia,SAU,1995,31.77333163,118.338773,23.885942,45.079162,682
Saudi Arabia,SAU,1996,26.2882102,124.0837931,23.885942,45.079162,682
Saudi Arabia,SAU,1997,21.29198942,129.4065463,23.885942,45.079162,682
Saudi Arabia,SAU,1998,16.96160989,134.0210172,23.885942,45.079162,682
Saudi Arabia,SAU,1999,13.44960281,138.0342549,23.885942,45.079162,682
Saudi Arabia,SAU,2000,10.81024363,140.2330556,23.885942,45.079162,682
Saudi Arabia,SAU,2001,8.759938105,140.3101178,23.885942,45.079162,682
Saudi Arabia,SAU,2002,7.041211438,140.4444793,23.885942,45.079162,682
Saudi Arabia,SAU,2003,5.612901886,140.69975,23.885942,45.079162,682
Saudi Arabia,SAU,2004,4.468088422,140.2119945,23.885942,45.079162,682
Saudi Arabia,SAU,2005,3.634874602,140.6641919,23.885942,45.079162,682
Saudi Arabia,SAU,2006,2.996653061,141.784074,23.885942,45.079162,682
Saudi Arabia,SAU,2007,2.441473878,142.8767589,23.885942,45.079162,682
Saudi Arabia,SAU,2008,1.970054933,143.0631465,23.885942,45.079162,682
Saudi Arabia,SAU,2009,1.574545964,141.2632571,23.885942,45.079162,682
Saudi Arabia,SAU,2010,1.27794833,139.4075762,23.885942,45.079162,682
Saudi Arabia,SAU,2011,1.040053948,136.3776458,23.885942,45.079162,682
Saudi Arabia,SAU,2012,0.844040208,133.4033702,23.885942,45.079162,682
Saudi Arabia,SAU,2013,0.688162213,131.0568551,23.885942,45.079162,682
Saudi Arabia,SAU,2014,0.560611461,128.1295612,23.885942,45.079162,682
Saudi Arabia,SAU,2015,0.462585626,126.1522141,23.885942,45.079162,682
Saudi Arabia,SAU,2016,0.385206415,122.6296693,23.885942,45.079162,682
Saudi Arabia,SAU,2017,0.324978249,118.9000579,23.885942,45.079162,682
Saudi Arabia,SAU,2018,0.272995014,115.5190506,23.885942,45.079162,682
Saudi Arabia,SAU,2019,0.230518702,112.7292344,23.885942,45.079162,682
Senegal,SEN,1990,186.8917085,29.50713886,14.497401,-14.452362,686
Senegal,SEN,1991,182.1180043,30.3264019,14.497401,-14.452362,686
Senegal,SEN,1992,176.862299,30.95991227,14.497401,-14.452362,686
Senegal,SEN,1993,172.2254733,31.67312231,14.497401,-14.452362,686
Senegal,SEN,1994,168.6265504,32.4975029,14.497401,-14.452362,686
Senegal,SEN,1995,161.6622089,32.6108017,14.497401,-14.452362,686
Senegal,SEN,1996,155.2517181,32.94937108,14.497401,-14.452362,686
Senegal,SEN,1997,150.0250908,33.75080499,14.497401,-14.452362,686
Senegal,SEN,1998,146.3189318,34.75688789,14.497401,-14.452362,686
Senegal,SEN,1999,142.8985908,35.45607297,14.497401,-14.452362,686
Senegal,SEN,2000,137.9409378,35.00369764,14.497401,-14.452362,686
Senegal,SEN,2001,149.5746314,38.63328895,14.497401,-14.452362,686
Senegal,SEN,2002,146.6801401,38.45599486,14.497401,-14.452362,686
Senegal,SEN,2003,138.2802854,36.83004331,14.497401,-14.452362,686
Senegal,SEN,2004,138.9341709,37.5435607,14.497401,-14.452362,686
Senegal,SEN,2005,136.6504226,37.36990717,14.497401,-14.452362,686
Senegal,SEN,2006,133.9689962,37.05008901,14.497401,-14.452362,686
Senegal,SEN,2007,132.35071,36.82651711,14.497401,-14.452362,686
Senegal,SEN,2008,132.3423403,36.86814594,14.497401,-14.452362,686
Senegal,SEN,2009,133.1038533,37.4094376,14.497401,-14.452362,686
Senegal,SEN,2010,125.8853293,35.94456733,14.497401,-14.452362,686
Senegal,SEN,2011,125.539562,37.06163978,14.497401,-14.452362,686
Senegal,SEN,2012,122.753287,38.05913353,14.497401,-14.452362,686
Senegal,SEN,2013,121.6288033,40.06331124,14.497401,-14.452362,686
Senegal,SEN,2014,121.6181582,42.21726327,14.497401,-14.452362,686
Senegal,SEN,2015,120.1145109,43.26332501,14.497401,-14.452362,686
Senegal,SEN,2016,118.4545623,43.47705808,14.497401,-14.452362,686
Senegal,SEN,2017,115.0797066,43.05243009,14.497401,-14.452362,686
Senegal,SEN,2018,110.9671545,42.98232671,14.497401,-14.452362,686
Senegal,SEN,2019,108.5836818,43.12451284,14.497401,-14.452362,686
Serbia,SRB,1990,69.15021437,95.62788028,44.016521,21.005859,688
Serbia,SRB,1991,65.73436359,94.9322499,44.016521,21.005859,688
Serbia,SRB,1992,64.6008312,97.88123967,44.016521,21.005859,688
Serbia,SRB,1993,64.03123656,101.2806996,44.016521,21.005859,688
Serbia,SRB,1994,63.02859541,103.9012152,44.016521,21.005859,688
Serbia,SRB,1995,62.21554226,107.105209,44.016521,21.005859,688
Serbia,SRB,1996,61.86492571,110.7844074,44.016521,21.005859,688
Serbia,SRB,1997,61.98795234,115.6830451,44.016521,21.005859,688
Serbia,SRB,1998,54.42803238,106.1891458,44.016521,21.005859,688
Serbia,SRB,1999,50.97619806,103.9299332,44.016521,21.005859,688
Serbia,SRB,2000,48.60587013,104.3490172,44.016521,21.005859,688
Serbia,SRB,2001,44.70500238,101.2839164,44.016521,21.005859,688
Serbia,SRB,2002,41.28923332,100.317814,44.016521,21.005859,688
Serbia,SRB,2003,39.12367647,101.3481264,44.016521,21.005859,688
Serbia,SRB,2004,36.72870374,101.4747453,44.016521,21.005859,688
Serbia,SRB,2005,34.93021474,102.3953573,44.016521,21.005859,688
Serbia,SRB,2006,32.01025821,100.4442007,44.016521,21.005859,688
Serbia,SRB,2007,29.28642197,98.84047279,44.016521,21.005859,688
Serbia,SRB,2008,27.31932937,99.0956368,44.016521,21.005859,688
Serbia,SRB,2009,25.19010858,97.28356281,44.016521,21.005859,688
Serbia,SRB,2010,22.74967139,93.1777472,44.016521,21.005859,688
Serbia,SRB,2011,20.58073641,88.71793381,44.016521,21.005859,688
Serbia,SRB,2012,18.78267972,85.36915688,44.016521,21.005859,688
Serbia,SRB,2013,17.51274925,83.55171116,44.016521,21.005859,688
Serbia,SRB,2014,16.61154638,82.26271084,44.016521,21.005859,688
Serbia,SRB,2015,15.73580629,80.08817295,44.016521,21.005859,688
Serbia,SRB,2016,14.58539425,75.09416952,44.016521,21.005859,688
Serbia,SRB,2017,14.02990182,73.05876319,44.016521,21.005859,688
Serbia,SRB,2018,13.5208106,71.66987706,44.016521,21.005859,688
Serbia,SRB,2019,12.90399819,70.17519241,44.016521,21.005859,688
Seychelles,SYC,1990,9.276030562,41.06372488,-4.679574,55.491977,690
Seychelles,SYC,1991,8.152861376,41.55159003,-4.679574,55.491977,690
Seychelles,SYC,1992,7.172570837,42.22951933,-4.679574,55.491977,690
Seychelles,SYC,1993,6.258086347,42.60692195,-4.679574,55.491977,690
Seychelles,SYC,1994,5.479905642,43.15223472,-4.679574,55.491977,690
Seychelles,SYC,1995,4.735653745,42.76513716,-4.679574,55.491977,690
Seychelles,SYC,1996,4.132405654,42.5491108,-4.679574,55.491977,690
Seychelles,SYC,1997,3.542836675,41.65151853,-4.679574,55.491977,690
Seychelles,SYC,1998,3.041817161,40.93251388,-4.679574,55.491977,690
Seychelles,SYC,1999,2.60880679,40.0535252,-4.679574,55.491977,690
Seychelles,SYC,2000,2.2453636,38.67469092,-4.679574,55.491977,690
Seychelles,SYC,2001,1.993233798,38.19070131,-4.679574,55.491977,690
Seychelles,SYC,2002,1.818551299,38.73985864,-4.679574,55.491977,690
Seychelles,SYC,2003,1.667252586,39.35426264,-4.679574,55.491977,690
Seychelles,SYC,2004,1.482625479,38.47250532,-4.679574,55.491977,690
Seychelles,SYC,2005,1.360968087,38.98639849,-4.679574,55.491977,690
Seychelles,SYC,2006,1.228159695,38.67647093,-4.679574,55.491977,690
Seychelles,SYC,2007,1.093239006,37.65673784,-4.679574,55.491977,690
Seychelles,SYC,2008,0.986996259,37.21690842,-4.679574,55.491977,690
Seychelles,SYC,2009,0.886816687,36.7214632,-4.679574,55.491977,690
Seychelles,SYC,2010,0.780419822,35.06441799,-4.679574,55.491977,690
Seychelles,SYC,2011,0.702797248,33.99711114,-4.679574,55.491977,690
Seychelles,SYC,2012,0.662124027,34.45559087,-4.679574,55.491977,690
Seychelles,SYC,2013,0.616068028,34.29535861,-4.679574,55.491977,690
Seychelles,SYC,2014,0.572816416,33.99870927,-4.679574,55.491977,690
Seychelles,SYC,2015,0.535143015,34.35632784,-4.679574,55.491977,690
Seychelles,SYC,2016,0.496183425,35.27527593,-4.679574,55.491977,690
Seychelles,SYC,2017,0.452972695,35.85406937,-4.679574,55.491977,690
Seychelles,SYC,2018,0.408649334,35.79534444,-4.679574,55.491977,690
Seychelles,SYC,2019,0.365469443,35.2437686,-4.679574,55.491977,690
Sierra Leone,SLE,1990,273.3718588,26.42403582,8.460555,-11.779889,694
Sierra Leone,SLE,1991,271.019383,25.73545954,8.460555,-11.779889,694
Sierra Leone,SLE,1992,265.8667421,24.89847321,8.460555,-11.779889,694
Sierra Leone,SLE,1993,259.8576049,24.14021728,8.460555,-11.779889,694
Sierra Leone,SLE,1994,255.7829346,23.58097235,8.460555,-11.779889,694
Sierra Leone,SLE,1995,252.3698273,23.19863469,8.460555,-11.779889,694
Sierra Leone,SLE,1996,250.3264567,23.29035002,8.460555,-11.779889,694
Sierra Leone,SLE,1997,252.0483972,24.02528745,8.460555,-11.779889,694
Sierra Leone,SLE,1998,248.6987161,24.5782403,8.460555,-11.779889,694
Sierra Leone,SLE,1999,244.6001249,24.72246397,8.460555,-11.779889,694
Sierra Leone,SLE,2000,243.3309506,24.79418421,8.460555,-11.779889,694
Sierra Leone,SLE,2001,241.5047273,25.04918606,8.460555,-11.779889,694
Sierra Leone,SLE,2002,242.1883067,25.5797855,8.460555,-11.779889,694
Sierra Leone,SLE,2003,240.9742,26.17491597,8.460555,-11.779889,694
Sierra Leone,SLE,2004,241.6425578,26.75798283,8.460555,-11.779889,694
Sierra Leone,SLE,2005,241.754332,27.51191216,8.460555,-11.779889,694
Sierra Leone,SLE,2006,239.9793645,28.15698424,8.460555,-11.779889,694
Sierra Leone,SLE,2007,236.142153,28.37541774,8.460555,-11.779889,694
Sierra Leone,SLE,2008,229.5661361,27.83489217,8.460555,-11.779889,694
Sierra Leone,SLE,2009,224.5160787,27.48022888,8.460555,-11.779889,694
Sierra Leone,SLE,2010,221.346686,27.96235022,8.460555,-11.779889,694
Sierra Leone,SLE,2011,214.815443,29.33054192,8.460555,-11.779889,694
Sierra Leone,SLE,2012,207.3798195,31.75215341,8.460555,-11.779889,694
Sierra Leone,SLE,2013,198.4402612,34.13944633,8.460555,-11.779889,694
Sierra Leone,SLE,2014,189.495497,35.49744353,8.460555,-11.779889,694
Sierra Leone,SLE,2015,185.1751828,36.115474,8.460555,-11.779889,694
Sierra Leone,SLE,2016,179.7095652,34.57128643,8.460555,-11.779889,694
Sierra Leone,SLE,2017,176.9632836,33.82744672,8.460555,-11.779889,694
Sierra Leone,SLE,2018,173.8222392,34.94409321,8.460555,-11.779889,694
Sierra Leone,SLE,2019,168.2734184,35.9940213,8.460555,-11.779889,694
Singapore,SGP,1990,3.579499817,59.97584109,1.352083,103.819836,702
Singapore,SGP,1991,2.945329854,54.53593259,1.352083,103.819836,702
Singapore,SGP,1992,2.425123827,50.31413256,1.352083,103.819836,702
Singapore,SGP,1993,2.007584041,47.18453087,1.352083,103.819836,702
Singapore,SGP,1994,1.681425595,45.65713825,1.352083,103.819836,702
Singapore,SGP,1995,1.413430011,44.02350805,1.352083,103.819836,702
Singapore,SGP,1996,1.179265805,43.25504495,1.352083,103.819836,702
Singapore,SGP,1997,0.970440118,41.76436184,1.352083,103.819836,702
Singapore,SGP,1998,0.798566855,40.56478219,1.352083,103.819836,702
Singapore,SGP,1999,0.647935581,37.61661383,1.352083,103.819836,702
Singapore,SGP,2000,0.525713871,35.42183172,1.352083,103.819836,702
Singapore,SGP,2001,0.429894676,33.26921687,1.352083,103.819836,702
Singapore,SGP,2002,0.355825,31.50685362,1.352083,103.819836,702
Singapore,SGP,2003,0.293858921,29.82061743,1.352083,103.819836,702
Singapore,SGP,2004,0.242837177,28.09791007,1.352083,103.819836,702
Singapore,SGP,2005,0.192891236,25.95485559,1.352083,103.819836,702
Singapore,SGP,2006,0.160487067,24.45126675,1.352083,103.819836,702
Singapore,SGP,2007,0.133496348,23.27087154,1.352083,103.819836,702
Singapore,SGP,2008,0.1103418,21.83296721,1.352083,103.819836,702
Singapore,SGP,2009,0.09045189,20.34936799,1.352083,103.819836,702
Singapore,SGP,2010,0.077076737,19.51542335,1.352083,103.819836,702
Singapore,SGP,2011,0.066710134,19.11694857,1.352083,103.819836,702
Singapore,SGP,2012,0.059467195,19.62869342,1.352083,103.819836,702
Singapore,SGP,2013,0.052844448,20.09359981,1.352083,103.819836,702
Singapore,SGP,2014,0.047301958,20.35441081,1.352083,103.819836,702
Singapore,SGP,2015,0.042287595,20.00133954,1.352083,103.819836,702
Singapore,SGP,2016,0.037833211,19.22685253,1.352083,103.819836,702
Singapore,SGP,2017,0.034423235,18.58003326,1.352083,103.819836,702
Singapore,SGP,2018,0.032232917,19.03397952,1.352083,103.819836,702
Singapore,SGP,2019,0.030003374,18.86700875,1.352083,103.819836,702
Slovakia,SVK,1990,3.581981391,100.9136468,48.669026,19.699024,703
Slovakia,SVK,1991,3.238022127,98.77853154,48.669026,19.699024,703
Slovakia,SVK,1992,2.894412533,95.90290785,48.669026,19.699024,703
Slovakia,SVK,1993,2.593543088,92.68047451,48.669026,19.699024,703
Slovakia,SVK,1994,2.305967918,88.64743225,48.669026,19.699024,703
Slovakia,SVK,1995,2.147986937,88.47071711,48.669026,19.699024,703
Slovakia,SVK,1996,1.917503748,83.53183483,48.669026,19.699024,703
Slovakia,SVK,1997,1.831579175,82.86924606,48.669026,19.699024,703
Slovakia,SVK,1998,1.686075056,79.40860583,48.669026,19.699024,703
Slovakia,SVK,1999,1.544365047,75.1780465,48.669026,19.699024,703
Slovakia,SVK,2000,1.393564097,70.9392545,48.669026,19.699024,703
Slovakia,SVK,2001,1.305201168,69.51057717,48.669026,19.699024,703
Slovakia,SVK,2002,1.205562068,67.82847251,48.669026,19.699024,703
Slovakia,SVK,2003,1.136800027,67.09617706,48.669026,19.699024,703
Slovakia,SVK,2004,1.056824751,65.11548911,48.669026,19.699024,703
Slovakia,SVK,2005,1.013029141,65.44484356,48.669026,19.699024,703
Slovakia,SVK,2006,0.946437996,63.9050911,48.669026,19.699024,703
Slovakia,SVK,2007,0.901223684,63.44743972,48.669026,19.699024,703
Slovakia,SVK,2008,0.817521726,60.39996008,48.669026,19.699024,703
Slovakia,SVK,2009,0.760533563,58.13952932,48.669026,19.699024,703
Slovakia,SVK,2010,0.68553315,54.65921503,48.669026,19.699024,703
Slovakia,SVK,2011,0.640116802,52.50412035,48.669026,19.699024,703
Slovakia,SVK,2012,0.586332043,49.32088435,48.669026,19.699024,703
Slovakia,SVK,2013,0.541410119,46.25858484,48.669026,19.699024,703
Slovakia,SVK,2014,0.502189194,43.66421939,48.669026,19.699024,703
Slovakia,SVK,2015,0.488807468,43.21022652,48.669026,19.699024,703
Slovakia,SVK,2016,0.448192357,40.23818421,48.669026,19.699024,703
Slovakia,SVK,2017,0.425935577,39.42910207,48.669026,19.699024,703
Slovakia,SVK,2018,0.40231473,39.14362912,48.669026,19.699024,703
Slovakia,SVK,2019,0.37925864,39.1518059,48.669026,19.699024,703
Slovenia,SVN,1990,11.4115856,57.96546608,46.151241,14.995463,705
Slovenia,SVN,1991,10.77171484,57.91301845,46.151241,14.995463,705
Slovenia,SVN,1992,10.11783082,57.51416279,46.151241,14.995463,705
Slovenia,SVN,1993,9.483618111,57.14159136,46.151241,14.995463,705
Slovenia,SVN,1994,8.833466486,56.3271361,46.151241,14.995463,705
Slovenia,SVN,1995,8.141205263,55.01884034,46.151241,14.995463,705
Slovenia,SVN,1996,7.570639449,53.47856541,46.151241,14.995463,705
Slovenia,SVN,1997,6.991219402,51.70896838,46.151241,14.995463,705
Slovenia,SVN,1998,6.42277146,49.34992947,46.151241,14.995463,705
Slovenia,SVN,1999,5.812809956,46.5303005,46.151241,14.995463,705
Slovenia,SVN,2000,5.166074625,43.05831398,46.151241,14.995463,705
Slovenia,SVN,2001,4.828765483,41.95851452,46.151241,14.995463,705
Slovenia,SVN,2002,4.326981177,39.35264123,46.151241,14.995463,705
Slovenia,SVN,2003,3.993929632,37.97416374,46.151241,14.995463,705
Slovenia,SVN,2004,3.672956358,35.70683058,46.151241,14.995463,705
Slovenia,SVN,2005,3.274110071,32.4785021,46.151241,14.995463,705
Slovenia,SVN,2006,3.005701139,30.88151404,46.151241,14.995463,705
Slovenia,SVN,2007,2.797597295,29.08596774,46.151241,14.995463,705
Slovenia,SVN,2008,2.571348882,27.09613913,46.151241,14.995463,705
Slovenia,SVN,2009,2.409941477,25.63458465,46.151241,14.995463,705
Slovenia,SVN,2010,2.262985872,24.62414663,46.151241,14.995463,705
Slovenia,SVN,2011,2.122811464,23.66051104,46.151241,14.995463,705
Slovenia,SVN,2012,2.019734065,23.14015002,46.151241,14.995463,705
Slovenia,SVN,2013,1.866052444,21.99435628,46.151241,14.995463,705
Slovenia,SVN,2014,1.655700504,19.99774157,46.151241,14.995463,705
Slovenia,SVN,2015,1.628774231,20.22015153,46.151241,14.995463,705
Slovenia,SVN,2016,1.513456302,19.00719272,46.151241,14.995463,705
Slovenia,SVN,2017,1.445119169,18.46418454,46.151241,14.995463,705
Slovenia,SVN,2018,1.373053537,18.57476686,46.151241,14.995463,705
Slovenia,SVN,2019,1.298704433,18.76118466,46.151241,14.995463,705
Solomon Islands,SLB,1990,510.8163649,17.1328735,-9.64571,160.156194,90
Solomon Islands,SLB,1991,507.5921488,17.85300233,-9.64571,160.156194,90
Solomon Islands,SLB,1992,502.6370331,18.49134105,-9.64571,160.156194,90
Solomon Islands,SLB,1993,497.3358267,19.08175991,-9.64571,160.156194,90
Solomon Islands,SLB,1994,492.6387038,19.60017527,-9.64571,160.156194,90
Solomon Islands,SLB,1995,487.4544088,20.03811563,-9.64571,160.156194,90
Solomon Islands,SLB,1996,483.8510904,20.5443662,-9.64571,160.156194,90
Solomon Islands,SLB,1997,481.6700311,21.07180633,-9.64571,160.156194,90
Solomon Islands,SLB,1998,480.5514516,21.60562483,-9.64571,160.156194,90
Solomon Islands,SLB,1999,477.7559589,21.98829419,-9.64571,160.156194,90
Solomon Islands,SLB,2000,474.9730601,22.24174261,-9.64571,160.156194,90
Solomon Islands,SLB,2001,471.2685611,22.37991281,-9.64571,160.156194,90
Solomon Islands,SLB,2002,466.8105218,22.41721436,-9.64571,160.156194,90
Solomon Islands,SLB,2003,463.8339812,22.53044881,-9.64571,160.156194,90
Solomon Islands,SLB,2004,460.9627802,22.65768731,-9.64571,160.156194,90
Solomon Islands,SLB,2005,459.5055564,22.97072202,-9.64571,160.156194,90
Solomon Islands,SLB,2006,458.6505325,23.61683253,-9.64571,160.156194,90
Solomon Islands,SLB,2007,452.5875219,24.35288494,-9.64571,160.156194,90
Solomon Islands,SLB,2008,435.2784458,24.64388985,-9.64571,160.156194,90
Solomon Islands,SLB,2009,438.3417092,26.0493766,-9.64571,160.156194,90
Solomon Islands,SLB,2010,432.3107879,26.81547435,-9.64571,160.156194,90
Solomon Islands,SLB,2011,437.20564,28.24355592,-9.64571,160.156194,90
Solomon Islands,SLB,2012,434.6495356,29.34476665,-9.64571,160.156194,90
Solomon Islands,SLB,2013,431.1530775,30.39864967,-9.64571,160.156194,90
Solomon Islands,SLB,2014,428.5746793,31.4539008,-9.64571,160.156194,90
Solomon Islands,SLB,2015,422.809822,32.10018543,-9.64571,160.156194,90
Solomon Islands,SLB,2016,412.8077377,32.22238382,-9.64571,160.156194,90
Solomon Islands,SLB,2017,407.015946,32.68489256,-9.64571,160.156194,90
Solomon Islands,SLB,2018,403.6330424,34.06396503,-9.64571,160.156194,90
Solomon Islands,SLB,2019,397.2595181,35.68982952,-9.64571,160.156194,90
Somalia,SOM,1990,346.7340769,7.52806648,5.152149,46.199616,706
Somalia,SOM,1991,339.2747114,6.904558655,5.152149,46.199616,706
Somalia,SOM,1992,332.4143732,6.480569461,5.152149,46.199616,706
Somalia,SOM,1993,327.5510214,6.216805304,5.152149,46.199616,706
Somalia,SOM,1994,324.6165694,6.057351088,5.152149,46.199616,706
Somalia,SOM,1995,322.1005965,6.003517755,5.152149,46.199616,706
Somalia,SOM,1996,319.8758208,6.156672061,5.152149,46.199616,706
Somalia,SOM,1997,317.6020666,6.735921425,5.152149,46.199616,706
Somalia,SOM,1998,314.6341303,7.412461824,5.152149,46.199616,706
Somalia,SOM,1999,310.5790877,8.02845393,5.152149,46.199616,706
Somalia,SOM,2000,306.8544105,8.082010963,5.152149,46.199616,706
Somalia,SOM,2001,302.5006958,7.814558958,5.152149,46.199616,706
Somalia,SOM,2002,301.422473,7.565801034,5.152149,46.199616,706
Somalia,SOM,2003,300.3711649,7.332133407,5.152149,46.199616,706
Somalia,SOM,2004,299.5561072,7.168184075,5.152149,46.199616,706
Somalia,SOM,2005,297.1254144,7.110717092,5.152149,46.199616,706
Somalia,SOM,2006,294.3345768,7.369847385,5.152149,46.199616,706
Somalia,SOM,2007,295.9403664,7.599137817,5.152149,46.199616,706
Somalia,SOM,2008,297.9725672,7.589756362,5.152149,46.199616,706
Somalia,SOM,2009,297.7756076,7.554416381,5.152149,46.199616,706
Somalia,SOM,2010,297.0319762,7.729089841,5.152149,46.199616,706
Somalia,SOM,2011,294.6559498,7.941845702,5.152149,46.199616,706
Somalia,SOM,2012,291.1928264,8.040541624,5.152149,46.199616,706
Somalia,SOM,2013,287.744241,8.215164457,5.152149,46.199616,706
Somalia,SOM,2014,285.1319479,8.280214786,5.152149,46.199616,706
Somalia,SOM,2015,282.6043917,8.52863429,5.152149,46.199616,706
Somalia,SOM,2016,280.1559014,8.510247949,5.152149,46.199616,706
Somalia,SOM,2017,276.9549352,8.572694458,5.152149,46.199616,706
Somalia,SOM,2018,275.1823727,9.266843376,5.152149,46.199616,706
Somalia,SOM,2019,272.0166274,9.450965859,5.152149,46.199616,706
South Africa,ZAF,1990,51.65362816,53.12073485,-30.559482,22.937506,710
South Africa,ZAF,1991,49.74734738,53.85788435,-30.559482,22.937506,710
South Africa,ZAF,1992,50.19498442,57.35465617,-30.559482,22.937506,710
South Africa,ZAF,1993,47.94696642,55.59627221,-30.559482,22.937506,710
South Africa,ZAF,1994,49.34265501,58.82511782,-30.559482,22.937506,710
South Africa,ZAF,1995,48.25477523,60.01185925,-30.559482,22.937506,710
South Africa,ZAF,1996,51.91725947,64.52068562,-30.559482,22.937506,710
South Africa,ZAF,1997,56.00551237,73.53221222,-30.559482,22.937506,710
South Africa,ZAF,1998,57.89395689,74.56133804,-30.559482,22.937506,710
South Africa,ZAF,1999,55.09956024,72.86416562,-30.559482,22.937506,710
South Africa,ZAF,2000,56.13322177,74.63930979,-30.559482,22.937506,710
South Africa,ZAF,2001,53.73836434,73.22933914,-30.559482,22.937506,710
South Africa,ZAF,2002,52.27290751,72.78021173,-30.559482,22.937506,710
South Africa,ZAF,2003,50.48848006,72.87608026,-30.559482,22.937506,710
South Africa,ZAF,2004,47.50175778,71.88536049,-30.559482,22.937506,710
South Africa,ZAF,2005,45.19241994,72.02473728,-30.559482,22.937506,710
South Africa,ZAF,2006,43.57618395,74.31554692,-30.559482,22.937506,710
South Africa,ZAF,2007,39.63972317,74.68592139,-30.559482,22.937506,710
South Africa,ZAF,2008,35.91221511,75.91838343,-30.559482,22.937506,710
South Africa,ZAF,2009,32.47985558,76.76775344,-30.559482,22.937506,710
South Africa,ZAF,2010,29.24495123,76.71289813,-30.559482,22.937506,710
South Africa,ZAF,2011,25.86022832,75.1055518,-30.559482,22.937506,710
South Africa,ZAF,2012,23.22691295,73.45681321,-30.559482,22.937506,710
South Africa,ZAF,2013,21.11749081,72.46079516,-30.559482,22.937506,710
South Africa,ZAF,2014,19.85984537,72.58903899,-30.559482,22.937506,710
South Africa,ZAF,2015,18.22018801,72.66838742,-30.559482,22.937506,710
South Africa,ZAF,2016,16.44530105,71.51314441,-30.559482,22.937506,710
South Africa,ZAF,2017,14.83247311,69.65082244,-30.559482,22.937506,710
South Africa,ZAF,2018,12.81133353,64.26601137,-30.559482,22.937506,710
South Africa,ZAF,2019,11.59852045,61.53435624,-30.559482,22.937506,710
South Korea,KOR,1990,2.272952617,73.42134314,35.907757,127.766922,410
South Korea,KOR,1991,1.847504778,70.43985213,35.907757,127.766922,410
South Korea,KOR,1992,1.457394452,66.63251226,35.907757,127.766922,410
South Korea,KOR,1993,1.142356263,63.62063853,35.907757,127.766922,410
South Korea,KOR,1994,0.899993611,61.21933121,35.907757,127.766922,410
South Korea,KOR,1995,0.708884041,57.63366882,35.907757,127.766922,410
South Korea,KOR,1996,0.572379108,54.97324146,35.907757,127.766922,410
South Korea,KOR,1997,0.470269527,53.60002973,35.907757,127.766922,410
South Korea,KOR,1998,0.391465302,52.78771308,35.907757,127.766922,410
South Korea,KOR,1999,0.328467198,52.04229279,35.907757,127.766922,410
South Korea,KOR,2000,0.272385009,49.8667579,35.907757,127.766922,410
South Korea,KOR,2001,0.222233078,46.86983187,35.907757,127.766922,410
South Korea,KOR,2002,0.182276777,44.68575912,35.907757,127.766922,410
South Korea,KOR,2003,0.148055669,42.72998968,35.907757,127.766922,410
South Korea,KOR,2004,0.119846639,40.6326399,35.907757,127.766922,410
South Korea,KOR,2005,0.098838578,38.40545226,35.907757,127.766922,410
South Korea,KOR,2006,0.082121275,35.9682727,35.907757,127.766922,410
South Korea,KOR,2007,0.068838893,33.82372531,35.907757,127.766922,410
South Korea,KOR,2008,0.057931827,31.91432943,35.907757,127.766922,410
South Korea,KOR,2009,0.049634825,30.28010228,35.907757,127.766922,410
South Korea,KOR,2010,0.043593944,29.20597207,35.907757,127.766922,410
South Korea,KOR,2011,0.038701321,28.66731075,35.907757,127.766922,410
South Korea,KOR,2012,0.034640179,28.78052495,35.907757,127.766922,410
South Korea,KOR,2013,0.030745169,28.6877283,35.907757,127.766922,410
South Korea,KOR,2014,0.027383678,28.3447099,35.907757,127.766922,410
South Korea,KOR,2015,0.024826304,28.08279832,35.907757,127.766922,410
South Korea,KOR,2016,0.022581941,27.36376178,35.907757,127.766922,410
South Korea,KOR,2017,0.021024636,27.28667103,35.907757,127.766922,410
South Korea,KOR,2018,0.019445617,27.33937526,35.907757,127.766922,410
South Korea,KOR,2019,0.018103763,27.85701315,35.907757,127.766922,410
Spain,ESP,1990,3.091311412,28.00529049,40.463667,-3.74922,724
Spain,ESP,1991,2.704154664,26.46279876,40.463667,-3.74922,724
Spain,ESP,1992,2.319595455,24.64650485,40.463667,-3.74922,724
Spain,ESP,1993,2.017791367,23.6792905,40.463667,-3.74922,724
Spain,ESP,1994,1.756993223,22.84606566,40.463667,-3.74922,724
Spain,ESP,1995,1.563103203,22.83319329,40.463667,-3.74922,724
Spain,ESP,1996,1.401189412,22.5997399,40.463667,-3.74922,724
Spain,ESP,1997,1.241337926,22.34401591,40.463667,-3.74922,724
Spain,ESP,1998,1.133230531,22.5708734,40.463667,-3.74922,724
Spain,ESP,1999,1.038858078,22.92282423,40.463667,-3.74922,724
Spain,ESP,2000,0.911818593,21.94936683,40.463667,-3.74922,724
Spain,ESP,2001,0.812726817,21.08239699,40.463667,-3.74922,724
Spain,ESP,2002,0.739125216,20.79147006,40.463667,-3.74922,724
Spain,ESP,2003,0.67778994,20.2838996,40.463667,-3.74922,724
Spain,ESP,2004,0.603654509,19.19820267,40.463667,-3.74922,724
Spain,ESP,2005,0.548271644,18.28271757,40.463667,-3.74922,724
Spain,ESP,2006,0.486857456,17.08991792,40.463667,-3.74922,724
Spain,ESP,2007,0.441774956,16.27018057,40.463667,-3.74922,724
Spain,ESP,2008,0.398246046,15.41245786,40.463667,-3.74922,724
Spain,ESP,2009,0.355154696,14.59311875,40.463667,-3.74922,724
Spain,ESP,2010,0.318026315,13.86712877,40.463667,-3.74922,724
Spain,ESP,2011,0.291538573,13.39267792,40.463667,-3.74922,724
Spain,ESP,2012,0.268814226,12.98747145,40.463667,-3.74922,724
Spain,ESP,2013,0.243482821,12.31657532,40.463667,-3.74922,724
Spain,ESP,2014,0.225501688,11.95141037,40.463667,-3.74922,724
Spain,ESP,2015,0.213240028,11.68613918,40.463667,-3.74922,724
Spain,ESP,2016,0.194041663,10.76385641,40.463667,-3.74922,724
Spain,ESP,2017,0.180765751,10.21851015,40.463667,-3.74922,724
Spain,ESP,2018,0.169626774,10.34704837,40.463667,-3.74922,724
Spain,ESP,2019,0.159730571,10.34083689,40.463667,-3.74922,724
Sri Lanka,LKA,1990,103.9517426,31.67585708,7.873054,80.771797,144
Sri Lanka,LKA,1991,94.56902048,29.51314389,7.873054,80.771797,144
Sri Lanka,LKA,1992,90.19445794,29.08602149,7.873054,80.771797,144
Sri Lanka,LKA,1993,83.20052328,27.81580645,7.873054,80.771797,144
Sri Lanka,LKA,1994,81.93575295,28.5832218,7.873054,80.771797,144
Sri Lanka,LKA,1995,81.04901857,29.76726813,7.873054,80.771797,144
Sri Lanka,LKA,1996,79.69695728,30.93263601,7.873054,80.771797,144
Sri Lanka,LKA,1997,80.86421348,33.74939703,7.873054,80.771797,144
Sri Lanka,LKA,1998,75.02777908,33.70228244,7.873054,80.771797,144
Sri Lanka,LKA,1999,72.61774525,35.09291941,7.873054,80.771797,144
Sri Lanka,LKA,2000,70.11954032,35.8672902,7.873054,80.771797,144
Sri Lanka,LKA,2001,65.07174962,34.96371735,7.873054,80.771797,144
Sri Lanka,LKA,2002,62.23666922,34.78789233,7.873054,80.771797,144
Sri Lanka,LKA,2003,61.97389025,36.20622202,7.873054,80.771797,144
Sri Lanka,LKA,2004,60.1434187,36.50589505,7.873054,80.771797,144
Sri Lanka,LKA,2005,59.82417545,37.94337325,7.873054,80.771797,144
Sri Lanka,LKA,2006,58.58961278,39.09305435,7.873054,80.771797,144
Sri Lanka,LKA,2007,56.19942732,39.81751067,7.873054,80.771797,144
Sri Lanka,LKA,2008,54.92191333,41.03695483,7.873054,80.771797,144
Sri Lanka,LKA,2009,53.13872702,41.04993797,7.873054,80.771797,144
Sri Lanka,LKA,2010,50.94270693,40.98850837,7.873054,80.771797,144
Sri Lanka,LKA,2011,49.29422915,40.63284327,7.873054,80.771797,144
Sri Lanka,LKA,2012,47.07955519,39.13404224,7.873054,80.771797,144
Sri Lanka,LKA,2013,44.31451578,36.39470936,7.873054,80.771797,144
Sri Lanka,LKA,2014,42.63214633,34.81897416,7.873054,80.771797,144
Sri Lanka,LKA,2015,39.62961116,33.24085499,7.873054,80.771797,144
Sri Lanka,LKA,2016,37.05690532,33.29505604,7.873054,80.771797,144
Sri Lanka,LKA,2017,34.51921999,33.92883515,7.873054,80.771797,144
Sri Lanka,LKA,2018,31.5711665,33.28655571,7.873054,80.771797,144
Sri Lanka,LKA,2019,29.61578356,33.31705726,7.873054,80.771797,144
Sudan,SDN,1990,261.5078012,33.75674029,12.862807,30.217636,729
Sudan,SDN,1991,255.4405563,33.54933137,12.862807,30.217636,729
Sudan,SDN,1992,249.4607498,33.55918066,12.862807,30.217636,729
Sudan,SDN,1993,243.232203,33.89894898,12.862807,30.217636,729
Sudan,SDN,1994,237.3055469,34.39486275,12.862807,30.217636,729
Sudan,SDN,1995,230.9965205,35.00301688,12.862807,30.217636,729
Sudan,SDN,1996,223.9182249,36.01989584,12.862807,30.217636,729
Sudan,SDN,1997,216.3544661,37.98084561,12.862807,30.217636,729
Sudan,SDN,1998,208.7548491,40.31426089,12.862807,30.217636,729
Sudan,SDN,1999,200.6491268,42.76686986,12.862807,30.217636,729
Sudan,SDN,2000,192.6357823,44.43421443,12.862807,30.217636,729
Sudan,SDN,2001,184.7318829,45.87498476,12.862807,30.217636,729
Sudan,SDN,2002,177.7337485,47.35355247,12.862807,30.217636,729
Sudan,SDN,2003,170.0442762,48.79092932,12.862807,30.217636,729
Sudan,SDN,2004,162.681313,50.43132142,12.862807,30.217636,729
Sudan,SDN,2005,155.7228821,52.49704989,12.862807,30.217636,729
Sudan,SDN,2006,148.2264548,54.90089952,12.862807,30.217636,729
Sudan,SDN,2007,140.293506,57.12687341,12.862807,30.217636,729
Sudan,SDN,2008,132.6814723,59.27465168,12.862807,30.217636,729
Sudan,SDN,2009,125.4505737,61.60994266,12.862807,30.217636,729
Sudan,SDN,2010,118.3673205,64.12317525,12.862807,30.217636,729
Sudan,SDN,2011,111.4399728,66.59644145,12.862807,30.217636,729
Sudan,SDN,2012,105.0861946,69.16078419,12.862807,30.217636,729
Sudan,SDN,2013,98.31328297,71.54455994,12.862807,30.217636,729
Sudan,SDN,2014,91.57140568,73.89044477,12.862807,30.217636,729
Sudan,SDN,2015,85.02773043,76.68952289,12.862807,30.217636,729
Sudan,SDN,2016,78.17504238,79.77348837,12.862807,30.217636,729
Sudan,SDN,2017,71.4618665,83.30642157,12.862807,30.217636,729
Sudan,SDN,2018,65.2711259,87.38378136,12.862807,30.217636,729
Sudan,SDN,2019,59.14216162,91.21301866,12.862807,30.217636,729
South Sudan,SSD,1990,221.0523761,23.64567071,,,
South Sudan,SSD,1991,218.5917155,23.17069662,,,
South Sudan,SSD,1992,216.7441754,22.75326959,,,
South Sudan,SSD,1993,214.1090248,22.4138497,,,
South Sudan,SSD,1994,210.9663958,22.07821399,,,
South Sudan,SSD,1995,209.4554448,21.94852806,,,
South Sudan,SSD,1996,205.0414296,21.90278833,,,
South Sudan,SSD,1997,198.4642849,22.40850368,,,
South Sudan,SSD,1998,193.7366698,23.23411006,,,
South Sudan,SSD,1999,188.1698432,23.76735909,,,
South Sudan,SSD,2000,183.5902323,23.42745902,,,
South Sudan,SSD,2001,177.5387714,22.91538484,,,
South Sudan,SSD,2002,174.0563594,22.6876379,,,
South Sudan,SSD,2003,171.7966501,22.90003848,,,
South Sudan,SSD,2004,170.2245829,23.21378919,,,
South Sudan,SSD,2005,168.637869,23.69386087,,,
South Sudan,SSD,2006,167.6744409,24.54110179,,,
South Sudan,SSD,2007,165.496638,24.93129272,,,
South Sudan,SSD,2008,163.4700877,25.12702128,,,
South Sudan,SSD,2009,160.7789008,25.19874625,,,
South Sudan,SSD,2010,157.7086175,25.40118706,,,
South Sudan,SSD,2011,154.7839397,25.93733309,,,
South Sudan,SSD,2012,152.4710768,26.59726146,,,
South Sudan,SSD,2013,150.6502495,27.62125196,,,
South Sudan,SSD,2014,148.2176306,28.06537219,,,
South Sudan,SSD,2015,147.6779665,28.71700414,,,
South Sudan,SSD,2016,145.4331141,28.37139062,,,
South Sudan,SSD,2017,140.0803189,27.82182715,,,
South Sudan,SSD,2018,136.3447106,27.63777447,,,
South Sudan,SSD,2019,133.2831353,27.62401245,,,
Suriname,SUR,1990,52.37314823,51.27250722,3.919305,-56.027783,740
Suriname,SUR,1991,52.32517241,53.87753392,3.919305,-56.027783,740
Suriname,SUR,1992,51.31146977,55.76579456,3.919305,-56.027783,740
Suriname,SUR,1993,51.72375588,59.78268,3.919305,-56.027783,740
Suriname,SUR,1994,45.48750775,55.74033797,3.919305,-56.027783,740
Suriname,SUR,1995,36.65978919,47.42279734,3.919305,-56.027783,740
Suriname,SUR,1996,33.80974559,46.81123957,3.919305,-56.027783,740
Suriname,SUR,1997,32.2016856,48.73134793,3.919305,-56.027783,740
Suriname,SUR,1998,32.36667867,53.76165633,3.919305,-56.027783,740
Suriname,SUR,1999,32.37029704,58.11259122,3.919305,-56.027783,740
Suriname,SUR,2000,31.32349362,60.07356869,3.919305,-56.027783,740
Suriname,SUR,2001,30.05209599,60.71905356,3.919305,-56.027783,740
Suriname,SUR,2002,28.54406485,60.02365469,3.919305,-56.027783,740
Suriname,SUR,2003,26.13730628,57.39873977,3.919305,-56.027783,740
Suriname,SUR,2004,23.85303973,54.53149033,3.919305,-56.027783,740
Suriname,SUR,2005,21.37184301,51.47306038,3.919305,-56.027783,740
Suriname,SUR,2006,19.37384512,49.17154418,3.919305,-56.027783,740
Suriname,SUR,2007,17.72962598,47.62129014,3.919305,-56.027783,740
Suriname,SUR,2008,16.48419833,46.89909807,3.919305,-56.027783,740
Suriname,SUR,2009,15.2905512,46.03788141,3.919305,-56.027783,740
Suriname,SUR,2010,14.09523613,45.34130895,3.919305,-56.027783,740
Suriname,SUR,2011,12.80285203,44.76666873,3.919305,-56.027783,740
Suriname,SUR,2012,11.68351017,45.5189238,3.919305,-56.027783,740
Suriname,SUR,2013,11.09673715,48.71739518,3.919305,-56.027783,740
Suriname,SUR,2014,10.62377403,51.85312723,3.919305,-56.027783,740
Suriname,SUR,2015,10.25388479,53.87613752,3.919305,-56.027783,740
Suriname,SUR,2016,9.772757146,51.652885,3.919305,-56.027783,740
Suriname,SUR,2017,9.284163197,48.34182897,3.919305,-56.027783,740
Suriname,SUR,2018,8.761259278,46.75350187,3.919305,-56.027783,740
Suriname,SUR,2019,8.188089785,45.42722429,3.919305,-56.027783,740
Sweden,SWE,1990,0.19593671,17.34462125,60.128161,18.643501,752
Sweden,SWE,1991,0.175860638,16.56048883,60.128161,18.643501,752
Sweden,SWE,1992,0.155559645,15.57339928,60.128161,18.643501,752
Sweden,SWE,1993,0.138846932,14.91932341,60.128161,18.643501,752
Sweden,SWE,1994,0.120451755,13.81402402,60.128161,18.643501,752
Sweden,SWE,1995,0.109200901,13.42421891,60.128161,18.643501,752
Sweden,SWE,1996,0.099914561,12.99951211,60.128161,18.643501,752
Sweden,SWE,1997,0.091331651,12.51625203,60.128161,18.643501,752
Sweden,SWE,1998,0.084291075,12.09335407,60.128161,18.643501,752
Sweden,SWE,1999,0.078247632,11.67853093,60.128161,18.643501,752
Sweden,SWE,2000,0.071430246,11.16355801,60.128161,18.643501,752
Sweden,SWE,2001,0.065187571,10.58019609,60.128161,18.643501,752
Sweden,SWE,2002,0.059153063,9.885548026,60.128161,18.643501,752
Sweden,SWE,2003,0.052724058,9.00284858,60.128161,18.643501,752
Sweden,SWE,2004,0.047594987,8.222295239,60.128161,18.643501,752
Sweden,SWE,2005,0.042972577,7.698402068,60.128161,18.643501,752
Sweden,SWE,2006,0.039896769,7.457548002,60.128161,18.643501,752
Sweden,SWE,2007,0.037108689,7.337920105,60.128161,18.643501,752
Sweden,SWE,2008,0.034359536,7.10150597,60.128161,18.643501,752
Sweden,SWE,2009,0.031922386,6.996137153,60.128161,18.643501,752
Sweden,SWE,2010,0.029208344,6.799665923,60.128161,18.643501,752
Sweden,SWE,2011,0.026485423,6.428854564,60.128161,18.643501,752
Sweden,SWE,2012,0.023303534,5.827333512,60.128161,18.643501,752
Sweden,SWE,2013,0.020067017,5.008460954,60.128161,18.643501,752
Sweden,SWE,2014,0.017186336,4.253113504,60.128161,18.643501,752
Sweden,SWE,2015,0.01533749,3.746703071,60.128161,18.643501,752
Sweden,SWE,2016,0.014189289,3.474993741,60.128161,18.643501,752
Sweden,SWE,2017,0.013321163,3.284965275,60.128161,18.643501,752
Sweden,SWE,2018,0.012586173,3.335905778,60.128161,18.643501,752
Sweden,SWE,2019,0.011735583,3.230732642,60.128161,18.643501,752
Switzerland,CHE,1990,0.053825615,34.68455219,46.818188,8.227512,756
Switzerland,CHE,1991,0.050506733,33.50951829,46.818188,8.227512,756
Switzerland,CHE,1992,0.046877864,31.89968293,46.818188,8.227512,756
Switzerland,CHE,1993,0.043528786,30.2445314,46.818188,8.227512,756
Switzerland,CHE,1994,0.040694335,29.01763105,46.818188,8.227512,756
Switzerland,CHE,1995,0.038995062,28.46265335,46.818188,8.227512,756
Switzerland,CHE,1996,0.036260678,26.8337263,46.818188,8.227512,756
Switzerland,CHE,1997,0.034293258,25.66834174,46.818188,8.227512,756
Switzerland,CHE,1998,0.032274975,24.35145446,46.818188,8.227512,756
Switzerland,CHE,1999,0.03029501,22.93698469,46.818188,8.227512,756
Switzerland,CHE,2000,0.028354011,21.57869635,46.818188,8.227512,756
Switzerland,CHE,2001,0.026049499,20.02707548,46.818188,8.227512,756
Switzerland,CHE,2002,0.024363842,19.2057359,46.818188,8.227512,756
Switzerland,CHE,2003,0.022709172,18.2321063,46.818188,8.227512,756
Switzerland,CHE,2004,0.020569943,16.92999757,46.818188,8.227512,756
Switzerland,CHE,2005,0.018862987,15.93462404,46.818188,8.227512,756
Switzerland,CHE,2006,0.017295107,15.27464948,46.818188,8.227512,756
Switzerland,CHE,2007,0.015863954,14.8155494,46.818188,8.227512,756
Switzerland,CHE,2008,0.014505622,14.33301714,46.818188,8.227512,756
Switzerland,CHE,2009,0.013409667,14.09099259,46.818188,8.227512,756
Switzerland,CHE,2010,0.012248698,13.56234526,46.818188,8.227512,756
Switzerland,CHE,2011,0.01130974,12.91297137,46.818188,8.227512,756
Switzerland,CHE,2012,0.010724648,12.46321514,46.818188,8.227512,756
Switzerland,CHE,2013,0.010132198,11.87111495,46.818188,8.227512,756
Switzerland,CHE,2014,0.009435008,11.14736339,46.818188,8.227512,756
Switzerland,CHE,2015,0.008833071,10.38894912,46.818188,8.227512,756
Switzerland,CHE,2016,0.008040466,9.057425851,46.818188,8.227512,756
Switzerland,CHE,2017,0.007473877,8.136155538,46.818188,8.227512,756
Switzerland,CHE,2018,0.007138062,8.212994575,46.818188,8.227512,756
Switzerland,CHE,2019,0.006922866,8.234928231,46.818188,8.227512,756
Syria,SYR,1990,19.66281172,114.4192727,34.802075,38.996815,760
Syria,SYR,1991,17.28660262,120.7216724,34.802075,38.996815,760
Syria,SYR,1992,15.30283724,129.1494042,34.802075,38.996815,760
Syria,SYR,1993,12.43838488,127.5876383,34.802075,38.996815,760
Syria,SYR,1994,10.46762535,129.6049595,34.802075,38.996815,760
Syria,SYR,1995,8.909803408,131.1490883,34.802075,38.996815,760
Syria,SYR,1996,7.475039401,129.3233064,34.802075,38.996815,760
Syria,SYR,1997,6.237518155,127.3888014,34.802075,38.996815,760
Syria,SYR,1998,5.310969348,128.232708,34.802075,38.996815,760
Syria,SYR,1999,4.303479318,123.5978667,34.802075,38.996815,760
Syria,SYR,2000,3.468198936,118.2502701,34.802075,38.996815,760
Syria,SYR,2001,2.769319029,112.5006863,34.802075,38.996815,760
Syria,SYR,2002,2.289109904,112.1643288,34.802075,38.996815,760
Syria,SYR,2003,1.780513021,106.1376494,34.802075,38.996815,760
Syria,SYR,2004,1.455240284,105.1880866,34.802075,38.996815,760
Syria,SYR,2005,1.187198825,103.6854468,34.802075,38.996815,760
Syria,SYR,2006,0.982913365,104.2563193,34.802075,38.996815,760
Syria,SYR,2007,0.81366499,107.6491981,34.802075,38.996815,760
Syria,SYR,2008,0.677098377,112.9859146,34.802075,38.996815,760
Syria,SYR,2009,0.548397466,112.8688691,34.802075,38.996815,760
Syria,SYR,2010,0.471169265,113.4785679,34.802075,38.996815,760
Syria,SYR,2011,0.421577978,113.4128391,34.802075,38.996815,760
Syria,SYR,2012,0.37922948,112.0373268,34.802075,38.996815,760
Syria,SYR,2013,0.348854024,111.5186002,34.802075,38.996815,760
Syria,SYR,2014,0.320309651,110.5251775,34.802075,38.996815,760
Syria,SYR,2015,0.287572356,108.5835103,34.802075,38.996815,760
Syria,SYR,2016,0.25852164,106.3386843,34.802075,38.996815,760
Syria,SYR,2017,0.229610088,103.8829602,34.802075,38.996815,760
Syria,SYR,2018,0.198657921,102.5950541,34.802075,38.996815,760
Syria,SYR,2019,0.167727135,101.7772371,34.802075,38.996815,760
Taiwan,TWN,1990,24.62296729,45.06743937,23.69781,120.960515,158
Taiwan,TWN,1991,21.67531534,43.93432096,23.69781,120.960515,158
Taiwan,TWN,1992,19.33162358,43.95238646,23.69781,120.960515,158
Taiwan,TWN,1993,17.01337929,43.40819714,23.69781,120.960515,158
Taiwan,TWN,1994,15.08766457,43.57749183,23.69781,120.960515,158
Taiwan,TWN,1995,13.54239316,44.09452593,23.69781,120.960515,158
Taiwan,TWN,1996,12.07934042,44.70488111,23.69781,120.960515,158
Taiwan,TWN,1997,10.31601436,44.09542968,23.69781,120.960515,158
Taiwan,TWN,1998,9.04380458,44.65257368,23.69781,120.960515,158
Taiwan,TWN,1999,7.774825078,44.34757989,23.69781,120.960515,158
Taiwan,TWN,2000,6.851663978,44.43063608,23.69781,120.960515,158
Taiwan,TWN,2001,6.03981347,43.99048644,23.69781,120.960515,158
Taiwan,TWN,2002,5.242925629,42.77169275,23.69781,120.960515,158
Taiwan,TWN,2003,4.629022281,41.90935865,23.69781,120.960515,158
Taiwan,TWN,2004,4.131791247,41.38170016,23.69781,120.960515,158
Taiwan,TWN,2005,3.73300173,40.81140425,23.69781,120.960515,158
Taiwan,TWN,2006,3.262814763,38.6142221,23.69781,120.960515,158
Taiwan,TWN,2007,2.951516384,37.27603138,23.69781,120.960515,158
Taiwan,TWN,2008,2.668702483,36.01613951,23.69781,120.960515,158
Taiwan,TWN,2009,2.385804341,33.99950513,23.69781,120.960515,158
Taiwan,TWN,2010,2.175105884,32.98540726,23.69781,120.960515,158
Taiwan,TWN,2011,2.070058472,33.79404254,23.69781,120.960515,158
Taiwan,TWN,2012,1.88973062,33.75699235,23.69781,120.960515,158
Taiwan,TWN,2013,1.719670396,33.73346195,23.69781,120.960515,158
Taiwan,TWN,2014,1.645934352,34.72202973,23.69781,120.960515,158
Taiwan,TWN,2015,1.536898567,33.75952452,23.69781,120.960515,158
Taiwan,TWN,2016,1.53333793,32.64718622,23.69781,120.960515,158
Taiwan,TWN,2017,1.497835271,31.03539683,23.69781,120.960515,158
Taiwan,TWN,2018,1.399487886,30.83353762,23.69781,120.960515,158
Taiwan,TWN,2019,1.245087003,30.63272652,23.69781,120.960515,158
Tajikistan,TJK,1990,141.0037406,54.39406682,38.861034,71.276093,762
Tajikistan,TJK,1991,141.7329913,56.8705071,38.861034,71.276093,762
Tajikistan,TJK,1992,146.6204192,60.99441499,38.861034,71.276093,762
Tajikistan,TJK,1993,150.4092369,64.40477757,38.861034,71.276093,762
Tajikistan,TJK,1994,161.2889484,71.7188425,38.861034,71.276093,762
Tajikistan,TJK,1995,152.4858379,70.36480686,38.861034,71.276093,762
Tajikistan,TJK,1996,144.4836834,68.47759606,38.861034,71.276093,762
Tajikistan,TJK,1997,143.5784085,69.05586247,38.861034,71.276093,762
Tajikistan,TJK,1998,148.0136889,72.12850967,38.861034,71.276093,762
Tajikistan,TJK,1999,148.8657239,74.03240244,38.861034,71.276093,762
Tajikistan,TJK,2000,148.2095748,75.31339126,38.861034,71.276093,762
Tajikistan,TJK,2001,146.3545997,76.79697617,38.861034,71.276093,762
Tajikistan,TJK,2002,140.9500593,78.63817273,38.861034,71.276093,762
Tajikistan,TJK,2003,133.8092927,80.71318339,38.861034,71.276093,762
Tajikistan,TJK,2004,126.9502054,83.10738093,38.861034,71.276093,762
Tajikistan,TJK,2005,122.6870827,86.39908508,38.861034,71.276093,762
Tajikistan,TJK,2006,117.870768,88.12250405,38.861034,71.276093,762
Tajikistan,TJK,2007,114.6499208,91.74138813,38.861034,71.276093,762
Tajikistan,TJK,2008,110.8781092,94.18685602,38.861034,71.276093,762
Tajikistan,TJK,2009,106.8276001,95.93024571,38.861034,71.276093,762
Tajikistan,TJK,2010,105.4223715,100.7051543,38.861034,71.276093,762
Tajikistan,TJK,2011,101.3960729,105.3552278,38.861034,71.276093,762
Tajikistan,TJK,2012,95.43975642,110.3749199,38.861034,71.276093,762
Tajikistan,TJK,2013,87.8904124,113.8479807,38.861034,71.276093,762
Tajikistan,TJK,2014,83.73514425,119.9754768,38.861034,71.276093,762
Tajikistan,TJK,2015,80.59404588,125.3675393,38.861034,71.276093,762
Tajikistan,TJK,2016,78.14494055,129.0686684,38.861034,71.276093,762
Tajikistan,TJK,2017,74.45609393,129.4756438,38.861034,71.276093,762
Tajikistan,TJK,2018,67.79448613,122.5272909,38.861034,71.276093,762
Tajikistan,TJK,2019,63.41455707,119.6798652,38.861034,71.276093,762
United Republic of Tanzania,TZA,1990,213.8350933,11.9315299,38.861034,71.276093,834
United Republic of Tanzania,TZA,1991,210.157296,11.90177758,38.861034,71.276093,834
United Republic of Tanzania,TZA,1992,207.5922761,11.97805495,38.861034,71.276093,834
United Republic of Tanzania,TZA,1993,205.2236672,12.11839842,38.861034,71.276093,834
United Republic of Tanzania,TZA,1994,203.0853442,12.31891038,38.861034,71.276093,834
United Republic of Tanzania,TZA,1995,200.4623321,12.56305041,38.861034,71.276093,834
United Republic of Tanzania,TZA,1996,197.0271718,12.85557848,38.861034,71.276093,834
United Republic of Tanzania,TZA,1997,194.4360987,13.42483753,38.861034,71.276093,834
United Republic of Tanzania,TZA,1998,192.5145298,14.07069925,38.861034,71.276093,834
United Republic of Tanzania,TZA,1999,187.9166362,14.58392265,38.861034,71.276093,834
United Republic of Tanzania,TZA,2000,182.1576391,14.73912623,38.861034,71.276093,834
United Republic of Tanzania,TZA,2001,176.2211328,14.83185037,38.861034,71.276093,834
United Republic of Tanzania,TZA,2002,172.984954,15.03162706,38.861034,71.276093,834
United Republic of Tanzania,TZA,2003,170.7335206,15.33562037,38.861034,71.276093,834
United Republic of Tanzania,TZA,2004,168.0973548,15.74247774,38.861034,71.276093,834
United Republic of Tanzania,TZA,2005,164.4532183,16.15628461,38.861034,71.276093,834
United Republic of Tanzania,TZA,2006,162.313693,16.9982909,38.861034,71.276093,834
United Republic of Tanzania,TZA,2007,159.6152073,17.51263337,38.861034,71.276093,834
United Republic of Tanzania,TZA,2008,156.2232953,17.94242119,38.861034,71.276093,834
United Republic of Tanzania,TZA,2009,153.6416574,18.50591036,38.861034,71.276093,834
United Republic of Tanzania,TZA,2010,150.1833442,19.01989335,38.861034,71.276093,834
United Republic of Tanzania,TZA,2011,147.5384384,19.7032833,38.861034,71.276093,834
United Republic of Tanzania,TZA,2012,146.333803,20.58529838,38.861034,71.276093,834
United Republic of Tanzania,TZA,2013,143.8553208,21.33827049,38.861034,71.276093,834
United Republic of Tanzania,TZA,2014,140.1489037,21.55481023,38.861034,71.276093,834
United Republic of Tanzania,TZA,2015,138.1052793,21.71988152,38.861034,71.276093,834
United Republic of Tanzania,TZA,2016,135.378802,21.24596433,38.861034,71.276093,834
United Republic of Tanzania,TZA,2017,132.7469187,20.88159285,38.861034,71.276093,834
United Republic of Tanzania,TZA,2018,129.9924278,21.34830125,38.861034,71.276093,834
United Republic of Tanzania,TZA,2019,126.7880426,21.96676317,38.861034,71.276093,834
Thailand,THA,1990,65.29755727,46.25242565,15.870032,100.992541,764
Thailand,THA,1991,63.22448777,47.72786172,15.870032,100.992541,764
Thailand,THA,1992,60.2491881,48.53941558,15.870032,100.992541,764
Thailand,THA,1993,57.01125746,49.10052645,15.870032,100.992541,764
Thailand,THA,1994,54.05204179,49.79474338,15.870032,100.992541,764
Thailand,THA,1995,50.86304036,50.32222576,15.870032,100.992541,764
Thailand,THA,1996,47.65220736,50.77220572,15.870032,100.992541,764
Thailand,THA,1997,41.26567915,47.49099998,15.870032,100.992541,764
Thailand,THA,1998,38.79681228,48.77827071,15.870032,100.992541,764
Thailand,THA,1999,37.58028387,51.27459827,15.870032,100.992541,764
Thailand,THA,2000,34.31481587,49.94873064,15.870032,100.992541,764
Thailand,THA,2001,29.95299684,46.4683515,15.870032,100.992541,764
Thailand,THA,2002,28.147089,46.4318057,15.870032,100.992541,764
Thailand,THA,2003,26.02694978,46.09818932,15.870032,100.992541,764
Thailand,THA,2004,24.76596024,46.43268155,15.870032,100.992541,764
Thailand,THA,2005,23.1429359,46.0181592,15.870032,100.992541,764
Thailand,THA,2006,21.27709531,45.0557021,15.870032,100.992541,764
Thailand,THA,2007,19.55921357,44.38394668,15.870032,100.992541,764
Thailand,THA,2008,18.00705416,43.79053863,15.870032,100.992541,764
Thailand,THA,2009,16.47122593,42.55496211,15.870032,100.992541,764
Thailand,THA,2010,15.3724994,42.44512552,15.870032,100.992541,764
Thailand,THA,2011,14.05583911,40.86098454,15.870032,100.992541,764
Thailand,THA,2012,12.85107254,38.66695625,15.870032,100.992541,764
Thailand,THA,2013,11.79615181,36.28408952,15.870032,100.992541,764
Thailand,THA,2014,11.03622518,34.76897512,15.870032,100.992541,764
Thailand,THA,2015,10.33296675,34.06259082,15.870032,100.992541,764
Thailand,THA,2016,9.83942471,33.93946653,15.870032,100.992541,764
Thailand,THA,2017,9.139449734,33.54956534,15.870032,100.992541,764
Thailand,THA,2018,8.450161459,34.09118843,15.870032,100.992541,764
Thailand,THA,2019,7.677639901,34.67956761,15.870032,100.992541,764
Timor,TLS,1990,225.5266012,11.22878513,-8.874217,125.727539,626
Timor,TLS,1991,222.3319982,11.2355443,-8.874217,125.727539,626
Timor,TLS,1992,221.2764729,11.22837655,-8.874217,125.727539,626
Timor,TLS,1993,219.855017,11.44056423,-8.874217,125.727539,626
Timor,TLS,1994,216.5495177,11.2746562,-8.874217,125.727539,626
Timor,TLS,1995,212.8983135,11.11208207,-8.874217,125.727539,626
Timor,TLS,1996,208.3587918,11.10986811,-8.874217,125.727539,626
Timor,TLS,1997,203.3336492,10.79475288,-8.874217,125.727539,626
Timor,TLS,1998,203.3298132,10.94168552,-8.874217,125.727539,626
Timor,TLS,1999,202.9221541,10.62996159,-8.874217,125.727539,626
Timor,TLS,2000,201.148346,10.51889586,-8.874217,125.727539,626
Timor,TLS,2001,197.597222,10.73360824,-8.874217,125.727539,626
Timor,TLS,2002,192.5408861,11.50513339,-8.874217,125.727539,626
Timor,TLS,2003,188.0262759,12.9119668,-8.874217,125.727539,626
Timor,TLS,2004,179.624044,14.00701084,-8.874217,125.727539,626
Timor,TLS,2005,172.0197784,15.17636102,-8.874217,125.727539,626
Timor,TLS,2006,163.3347643,16.22514326,-8.874217,125.727539,626
Timor,TLS,2007,156.974365,17.6876526,-8.874217,125.727539,626
Timor,TLS,2008,150.1405834,19.13224991,-8.874217,125.727539,626
Timor,TLS,2009,147.5374517,20.7739952,-8.874217,125.727539,626
Timor,TLS,2010,144.5884153,22.23034993,-8.874217,125.727539,626
Timor,TLS,2011,144.6124115,23.9545214,-8.874217,125.727539,626
Timor,TLS,2012,143.4686734,25.3537876,-8.874217,125.727539,626
Timor,TLS,2013,142.1970145,26.36716872,-8.874217,125.727539,626
Timor,TLS,2014,141.1127632,26.99697061,-8.874217,125.727539,626
Timor,TLS,2015,139.2417048,27.26317015,-8.874217,125.727539,626
Timor,TLS,2016,137.7336985,27.46820298,-8.874217,125.727539,626
Timor,TLS,2017,136.7242249,27.38047014,-8.874217,125.727539,626
Timor,TLS,2018,135.7228823,28.85323018,-8.874217,125.727539,626
Timor,TLS,2019,134.4319501,29.32281367,-8.874217,125.727539,626
Togo,TGO,1990,211.5735556,29.48272729,8.619543,0.824782,768
Togo,TGO,1991,209.2256555,29.43745834,8.619543,0.824782,768
Togo,TGO,1992,206.9548752,29.43948414,8.619543,0.824782,768
Togo,TGO,1993,205.3350919,29.6710842,8.619543,0.824782,768
Togo,TGO,1994,203.8546056,29.88561649,8.619543,0.824782,768
Togo,TGO,1995,201.9761505,30.3416736,8.619543,0.824782,768
Togo,TGO,1996,200.0652598,31.50520858,8.619543,0.824782,768
Togo,TGO,1997,197.7298052,33.43854644,8.619543,0.824782,768
Togo,TGO,1998,194.9166309,35.41812764,8.619543,0.824782,768
Togo,TGO,1999,189.9974986,36.3454368,8.619543,0.824782,768
Togo,TGO,2000,188.2882497,36.55907887,8.619543,0.824782,768
Togo,TGO,2001,187.0801592,36.01427968,8.619543,0.824782,768
Togo,TGO,2002,187.4980867,35.13961005,8.619543,0.824782,768
Togo,TGO,2003,186.9516596,34.24445787,8.619543,0.824782,768
Togo,TGO,2004,184.2702164,33.18615365,8.619543,0.824782,768
Togo,TGO,2005,182.9270571,33.15398171,8.619543,0.824782,768
Togo,TGO,2006,181.480689,33.84583242,8.619543,0.824782,768
Togo,TGO,2007,179.1670069,34.14491239,8.619543,0.824782,768
Togo,TGO,2008,179.1168203,34.83959947,8.619543,0.824782,768
Togo,TGO,2009,176.9165311,35.33000734,8.619543,0.824782,768
Togo,TGO,2010,173.2678962,36.29465649,8.619543,0.824782,768
Togo,TGO,2011,168.4735849,37.92607534,8.619543,0.824782,768
Togo,TGO,2012,161.8272918,40.2024953,8.619543,0.824782,768
Togo,TGO,2013,155.1583683,42.61004084,8.619543,0.824782,768
Togo,TGO,2014,149.1040212,44.30188591,8.619543,0.824782,768
Togo,TGO,2015,146.1759926,45.41964388,8.619543,0.824782,768
Togo,TGO,2016,143.1309663,44.45080945,8.619543,0.824782,768
Togo,TGO,2017,140.6746761,43.9366168,8.619543,0.824782,768
Togo,TGO,2018,136.2495469,44.51366074,8.619543,0.824782,768
Togo,TGO,2019,131.6002724,45.62925294,8.619543,0.824782,768
Tokelau,TKL,1990,0.928869284,25.01217023,-8.967363,-171.855881,772
Tokelau,TKL,1991,0.859156117,25.7186629,-8.967363,-171.855881,772
Tokelau,TKL,1992,0.789950798,26.41404859,-8.967363,-171.855881,772
Tokelau,TKL,1993,0.721850294,26.88563219,-8.967363,-171.855881,772
Tokelau,TKL,1994,0.655558544,26.34619391,-8.967363,-171.855881,772
Tokelau,TKL,1995,0.59158608,25.68266081,-8.967363,-171.855881,772
Tokelau,TKL,1996,0.527109847,24.85051647,-8.967363,-171.855881,772
Tokelau,TKL,1997,0.462292156,23.78877143,-8.967363,-171.855881,772
Tokelau,TKL,1998,0.401062318,22.34318461,-8.967363,-171.855881,772
Tokelau,TKL,1999,0.348053279,20.77819034,-8.967363,-171.855881,772
Tokelau,TKL,2000,0.308188893,19.58659872,-8.967363,-171.855881,772
Tokelau,TKL,2001,0.279022842,19.37624287,-8.967363,-171.855881,772
Tokelau,TKL,2002,0.254245862,19.66982832,-8.967363,-171.855881,772
Tokelau,TKL,2003,0.232852134,19.92285904,-8.967363,-171.855881,772
Tokelau,TKL,2004,0.213433123,20.18436369,-8.967363,-171.855881,772
Tokelau,TKL,2005,0.194917881,20.1500009,-8.967363,-171.855881,772
Tokelau,TKL,2006,0.176563733,20.01468878,-8.967363,-171.855881,772
Tokelau,TKL,2007,0.159401182,19.31774775,-8.967363,-171.855881,772
Tokelau,TKL,2008,0.143678606,18.58759431,-8.967363,-171.855881,772
Tokelau,TKL,2009,0.129470975,17.77158625,-8.967363,-171.855881,772
Tokelau,TKL,2010,0.116989281,17.2766937,-8.967363,-171.855881,772
Tokelau,TKL,2011,0.105949279,16.89045221,-8.967363,-171.855881,772
Tokelau,TKL,2012,0.095560896,16.58152751,-8.967363,-171.855881,772
Tokelau,TKL,2013,0.086214616,16.47583859,-8.967363,-171.855881,772
Tokelau,TKL,2014,0.078390496,16.26907517,-8.967363,-171.855881,772
Tokelau,TKL,2015,0.071997554,16.1430523,-8.967363,-171.855881,772
Tokelau,TKL,2016,0.067383843,16.84834094,-8.967363,-171.855881,772
Tokelau,TKL,2017,0.06298709,17.42356219,-8.967363,-171.855881,772
Tokelau,TKL,2018,0.057440917,17.67634632,-8.967363,-171.855881,772
Tokelau,TKL,2019,0.051030668,17.53490758,-8.967363,-171.855881,772
Tonga,TON,1990,102.9842838,19.09290226,-21.178986,-175.198242,776
Tonga,TON,1991,98.61666025,19.79364864,-21.178986,-175.198242,776
Tonga,TON,1992,93.4458524,20.33777965,-21.178986,-175.198242,776
Tonga,TON,1993,90.93848891,21.33701564,-21.178986,-175.198242,776
Tonga,TON,1994,88.04256524,21.54869535,-21.178986,-175.198242,776
Tonga,TON,1995,83.20459771,21.15712364,-21.178986,-175.198242,776
Tonga,TON,1996,80.56406046,21.72799179,-21.178986,-175.198242,776
Tonga,TON,1997,79.70623487,23.17397467,-21.178986,-175.198242,776
Tonga,TON,1998,80.74912567,25.28680668,-21.178986,-175.198242,776
Tonga,TON,1999,80.9484047,26.94210333,-21.178986,-175.198242,776
Tonga,TON,2000,77.54787776,26.66622808,-21.178986,-175.198242,776
Tonga,TON,2001,73.85418059,26.11477575,-21.178986,-175.198242,776
Tonga,TON,2002,71.69861053,26.32766426,-21.178986,-175.198242,776
Tonga,TON,2003,69.68988226,26.37776154,-21.178986,-175.198242,776
Tonga,TON,2004,66.11135291,25.69436806,-21.178986,-175.198242,776
Tonga,TON,2005,61.69811991,24.33442534,-21.178986,-175.198242,776
Tonga,TON,2006,60.46976635,24.58946102,-21.178986,-175.198242,776
Tonga,TON,2007,60.12911067,24.86113072,-21.178986,-175.198242,776
Tonga,TON,2008,59.79539419,25.16912822,-21.178986,-175.198242,776
Tonga,TON,2009,59.21016857,25.27426477,-21.178986,-175.198242,776
Tonga,TON,2010,58.34532109,25.38102564,-21.178986,-175.198242,776
Tonga,TON,2011,56.96902503,25.40823061,-21.178986,-175.198242,776
Tonga,TON,2012,55.13044374,25.44162045,-21.178986,-175.198242,776
Tonga,TON,2013,53.10261332,25.69995718,-21.178986,-175.198242,776
Tonga,TON,2014,50.91869325,25.79647776,-21.178986,-175.198242,776
Tonga,TON,2015,48.70355717,25.95502808,-21.178986,-175.198242,776
Tonga,TON,2016,46.37944118,26.42587161,-21.178986,-175.198242,776
Tonga,TON,2017,43.91634396,26.69616756,-21.178986,-175.198242,776
Tonga,TON,2018,41.53286343,27.040458,-21.178986,-175.198242,776
Tonga,TON,2019,39.13313215,26.94417226,-21.178986,-175.198242,776
Trinidad and Tobago,TTO,1990,1.382555049,79.04445041,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1991,1.2808678,77.55822614,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1992,1.203301845,77.81974512,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1993,1.159731367,79.98953125,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1994,1.091996821,80.86732927,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1995,0.969798313,76.5387026,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1996,0.909009742,78.26310052,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1997,0.796881838,74.18320043,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1998,0.74947663,76.369623,10.691803,-61.222503,780
Trinidad and Tobago,TTO,1999,0.678629978,75.90544952,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2000,0.571750249,70.01765627,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2001,0.505123074,68.13903614,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2002,0.430056014,63.86978109,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2003,0.383832513,62.98513408,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2004,0.322375215,58.56037694,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2005,0.275094218,55.4666991,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2006,0.236351168,52.59076817,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2007,0.207941658,51.5797873,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2008,0.190108862,52.85109987,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2009,0.162111823,49.80477963,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2010,0.143678623,48.5945981,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2011,0.126412462,46.91583732,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2012,0.111773905,45.60418651,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2013,0.106788842,47.66099934,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2014,0.101107294,49.03670906,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2015,0.095395663,49.67230345,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2016,0.091949052,49.74391363,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2017,0.087317292,48.79632941,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2018,0.08251966,49.04888223,10.691803,-61.222503,780
Trinidad and Tobago,TTO,2019,0.077680982,49.87263021,10.691803,-61.222503,780
Tunisia,TUN,1990,21.04575557,69.39836884,33.886917,9.537499,788
Tunisia,TUN,1991,19.44119043,71.83717204,33.886917,9.537499,788
Tunisia,TUN,1992,17.3605947,72.33069995,33.886917,9.537499,788
Tunisia,TUN,1993,15.43835408,73.39057258,33.886917,9.537499,788
Tunisia,TUN,1994,13.42126087,73.21232225,33.886917,9.537499,788
Tunisia,TUN,1995,12.17360187,76.58834817,33.886917,9.537499,788
Tunisia,TUN,1996,10.5174677,78.01611357,33.886917,9.537499,788
Tunisia,TUN,1997,8.995797431,80.92044589,33.886917,9.537499,788
Tunisia,TUN,1998,7.598529034,84.00263985,33.886917,9.537499,788
Tunisia,TUN,1999,6.317222753,85.9438276,33.886917,9.537499,788
Tunisia,TUN,2000,5.244269759,85.75090136,33.886917,9.537499,788
Tunisia,TUN,2001,4.342323284,84.39270572,33.886917,9.537499,788
Tunisia,TUN,2002,3.531284197,82.78553315,33.886917,9.537499,788
Tunisia,TUN,2003,2.830069815,81.30256294,33.886917,9.537499,788
Tunisia,TUN,2004,2.251379657,79.75102883,33.886917,9.537499,788
Tunisia,TUN,2005,1.819616327,78.25529589,33.886917,9.537499,788
Tunisia,TUN,2006,1.487537489,77.70520069,33.886917,9.537499,788
Tunisia,TUN,2007,1.204544212,77.65109166,33.886917,9.537499,788
Tunisia,TUN,2008,0.971930668,78.14657596,33.886917,9.537499,788
Tunisia,TUN,2009,0.787347885,78.27524878,33.886917,9.537499,788
Tunisia,TUN,2010,0.657336455,78.19813014,33.886917,9.537499,788
Tunisia,TUN,2011,0.561538962,76.66077145,33.886917,9.537499,788
Tunisia,TUN,2012,0.484659837,74.8444664,33.886917,9.537499,788
Tunisia,TUN,2013,0.423502294,73.13911847,33.886917,9.537499,788
Tunisia,TUN,2014,0.370656418,71.16237458,33.886917,9.537499,788
Tunisia,TUN,2015,0.323519815,69.44602236,33.886917,9.537499,788
Tunisia,TUN,2016,0.283931099,67.60286397,33.886917,9.537499,788
Tunisia,TUN,2017,0.249548733,66.34008306,33.886917,9.537499,788
Tunisia,TUN,2018,0.215714765,65.78268312,33.886917,9.537499,788
Tunisia,TUN,2019,0.184077469,65.40610601,33.886917,9.537499,788
Turkey,TUR,1990,24.5144939,79.02089528,38.963745,35.243322,792
Turkey,TUR,1991,21.19516336,78.45400299,38.963745,35.243322,792
Turkey,TUR,1992,18.15472282,77.97456621,38.963745,35.243322,792
Turkey,TUR,1993,15.52758865,77.89737546,38.963745,35.243322,792
Turkey,TUR,1994,13.32764495,77.88116363,38.963745,35.243322,792
Turkey,TUR,1995,11.36285167,77.33480441,38.963745,35.243322,792
Turkey,TUR,1996,9.481649077,74.91529338,38.963745,35.243322,792
Turkey,TUR,1997,8.003176468,74.47211837,38.963745,35.243322,792
Turkey,TUR,1998,6.620379505,72.39714062,38.963745,35.243322,792
Turkey,TUR,1999,5.320272902,67.94384923,38.963745,35.243322,792
Turkey,TUR,2000,4.257174012,62.82329059,38.963745,35.243322,792
Turkey,TUR,2001,3.64911846,62.74247423,38.963745,35.243322,792
Turkey,TUR,2002,3.137611493,63.59338161,38.963745,35.243322,792
Turkey,TUR,2003,2.622794258,61.89987399,38.963745,35.243322,792
Turkey,TUR,2004,2.181063979,59.57065989,38.963745,35.243322,792
Turkey,TUR,2005,1.832854962,56.99024118,38.963745,35.243322,792
Turkey,TUR,2006,1.614594939,57.83408925,38.963745,35.243322,792
Turkey,TUR,2007,1.433375528,59.66785286,38.963745,35.243322,792
Turkey,TUR,2008,1.292056277,62.62494465,38.963745,35.243322,792
Turkey,TUR,2009,1.178187425,65.85465675,38.963745,35.243322,792
Turkey,TUR,2010,1.043963075,66.47023276,38.963745,35.243322,792
Turkey,TUR,2011,0.91184551,65.97541709,38.963745,35.243322,792
Turkey,TUR,2012,0.793762596,65.15133812,38.963745,35.243322,792
Turkey,TUR,2013,0.702002989,65.15171522,38.963745,35.243322,792
Turkey,TUR,2014,0.616014591,64.31494579,38.963745,35.243322,792
Turkey,TUR,2015,0.529377312,62.53611449,38.963745,35.243322,792
Turkey,TUR,2016,0.459990592,59.87304504,38.963745,35.243322,792
Turkey,TUR,2017,0.398389579,57.11626365,38.963745,35.243322,792
Turkey,TUR,2018,0.336864927,54.85001533,38.963745,35.243322,792
Turkey,TUR,2019,0.286465324,53.68670211,38.963745,35.243322,792
Turkmenistan,TKM,1990,2.331237202,110.2049684,38.969719,59.556278,795
Turkmenistan,TKM,1991,2.301266321,115.7085593,38.969719,59.556278,795
Turkmenistan,TKM,1992,2.245670126,119.5243752,38.969719,59.556278,795
Turkmenistan,TKM,1993,2.372399032,135.8997838,38.969719,59.556278,795
Turkmenistan,TKM,1994,2.305770923,142.1123722,38.969719,59.556278,795
Turkmenistan,TKM,1995,2.126456616,141.4878287,38.969719,59.556278,795
Turkmenistan,TKM,1996,1.990006973,145.9121113,38.969719,59.556278,795
Turkmenistan,TKM,1997,1.751095698,144.1587462,38.969719,59.556278,795
Turkmenistan,TKM,1998,1.496210511,140.0393251,38.969719,59.556278,795
Turkmenistan,TKM,1999,1.276086672,134.074682,38.969719,59.556278,795
Turkmenistan,TKM,2000,1.124303896,128.5899464,38.969719,59.556278,795
Turkmenistan,TKM,2001,1.053902219,124.4783147,38.969719,59.556278,795
Turkmenistan,TKM,2002,1.037541002,122.3221289,38.969719,59.556278,795
Turkmenistan,TKM,2003,1.016483245,118.1941323,38.969719,59.556278,795
Turkmenistan,TKM,2004,1.007708506,116.1927842,38.969719,59.556278,795
Turkmenistan,TKM,2005,0.988563173,117.4849679,38.969719,59.556278,795
Turkmenistan,TKM,2006,0.904664714,116.5442862,38.969719,59.556278,795
Turkmenistan,TKM,2007,0.80067865,116.5634224,38.969719,59.556278,795
Turkmenistan,TKM,2008,0.683628724,114.4096382,38.969719,59.556278,795
Turkmenistan,TKM,2009,0.545079934,105.4975162,38.969719,59.556278,795
Turkmenistan,TKM,2010,0.458815953,102.2968528,38.969719,59.556278,795
Turkmenistan,TKM,2011,0.40304149,103.9794086,38.969719,59.556278,795
Turkmenistan,TKM,2012,0.341350333,104.692379,38.969719,59.556278,795
Turkmenistan,TKM,2013,0.287280014,106.9430381,38.969719,59.556278,795
Turkmenistan,TKM,2014,0.241591575,108.3670034,38.969719,59.556278,795
Turkmenistan,TKM,2015,0.208596132,108.8379539,38.969719,59.556278,795
Turkmenistan,TKM,2016,0.18511943,105.8018665,38.969719,59.556278,795
Turkmenistan,TKM,2017,0.167206244,101.7920601,38.969719,59.556278,795
Turkmenistan,TKM,2018,0.155463365,100.7983411,38.969719,59.556278,795
Turkmenistan,TKM,2019,0.144057384,98.56573118,38.969719,59.556278,795
Tuvalu,TUV,1990,167.1633997,16.2420995,-7.109535,177.64933,798
Tuvalu,TUV,1991,157.4845833,16.93369691,-7.109535,177.64933,798
Tuvalu,TUV,1992,148.3383244,17.62479307,-7.109535,177.64933,798
Tuvalu,TUV,1993,139.7665053,18.21857076,-7.109535,177.64933,798
Tuvalu,TUV,1994,130.4023336,18.56741248,-7.109535,177.64933,798
Tuvalu,TUV,1995,123.5102728,19.0924936,-7.109535,177.64933,798
Tuvalu,TUV,1996,116.6628164,19.50982594,-7.109535,177.64933,798
Tuvalu,TUV,1997,110.464676,20.02116683,-7.109535,177.64933,798
Tuvalu,TUV,1998,103.0441352,20.20881028,-7.109535,177.64933,798
Tuvalu,TUV,1999,96.47832145,20.4305312,-7.109535,177.64933,798
Tuvalu,TUV,2000,89.68471745,20.44536978,-7.109535,177.64933,798
Tuvalu,TUV,2001,82.83737012,20.54714867,-7.109535,177.64933,798
Tuvalu,TUV,2002,76.29628138,20.74220682,-7.109535,177.64933,798
Tuvalu,TUV,2003,70.36216717,21.02681903,-7.109535,177.64933,798
Tuvalu,TUV,2004,64.76618153,21.23707956,-7.109535,177.64933,798
Tuvalu,TUV,2005,59.8022936,21.33509555,-7.109535,177.64933,798
Tuvalu,TUV,2006,55.14870893,21.34069191,-7.109535,177.64933,798
Tuvalu,TUV,2007,50.75351259,21.24209041,-7.109535,177.64933,798
Tuvalu,TUV,2008,46.50235727,21.04419381,-7.109535,177.64933,798
Tuvalu,TUV,2009,42.5995497,20.84861658,-7.109535,177.64933,798
Tuvalu,TUV,2010,39.17204214,20.67244444,-7.109535,177.64933,798
Tuvalu,TUV,2011,36.02874003,20.57640416,-7.109535,177.64933,798
Tuvalu,TUV,2012,33.13603719,20.53146335,-7.109535,177.64933,798
Tuvalu,TUV,2013,30.4245771,20.54373159,-7.109535,177.64933,798
Tuvalu,TUV,2014,27.90393809,20.60437938,-7.109535,177.64933,798
Tuvalu,TUV,2015,25.51639956,20.62266348,-7.109535,177.64933,798
Tuvalu,TUV,2016,23.36239929,21.42627414,-7.109535,177.64933,798
Tuvalu,TUV,2017,21.38424679,21.96416517,-7.109535,177.64933,798
Tuvalu,TUV,2018,19.47724364,22.21764962,-7.109535,177.64933,798
Tuvalu,TUV,2019,17.63732147,22.04354504,-7.109535,177.64933,798
Uganda,UGA,1990,207.4021175,12.8737233,1.373333,32.290275,800
Uganda,UGA,1991,210.9432732,13.05489263,1.373333,32.290275,800
Uganda,UGA,1992,211.9948769,13.10796979,1.373333,32.290275,800
Uganda,UGA,1993,214.8134422,13.19626285,1.373333,32.290275,800
Uganda,UGA,1994,216.9330028,13.4267767,1.373333,32.290275,800
Uganda,UGA,1995,218.6101227,13.78570425,1.373333,32.290275,800
Uganda,UGA,1996,219.4272727,14.26189725,1.373333,32.290275,800
Uganda,UGA,1997,217.9358139,14.98774957,1.373333,32.290275,800
Uganda,UGA,1998,216.7328168,15.8300533,1.373333,32.290275,800
Uganda,UGA,1999,213.9970703,16.79861752,1.373333,32.290275,800
Uganda,UGA,2000,212.3909933,17.32381645,1.373333,32.290275,800
Uganda,UGA,2001,208.3795117,17.77572113,1.373333,32.290275,800
Uganda,UGA,2002,202.9291102,17.85423603,1.373333,32.290275,800
Uganda,UGA,2003,196.1504073,18.06397045,1.373333,32.290275,800
Uganda,UGA,2004,191.530835,18.59143211,1.373333,32.290275,800
Uganda,UGA,2005,185.7759777,19.32190335,1.373333,32.290275,800
Uganda,UGA,2006,179.3581373,20.34125882,1.373333,32.290275,800
Uganda,UGA,2007,172.0762581,20.85858042,1.373333,32.290275,800
Uganda,UGA,2008,164.6650042,21.09941856,1.373333,32.290275,800
Uganda,UGA,2009,158.7072908,21.7143415,1.373333,32.290275,800
Uganda,UGA,2010,154.1113704,22.76831491,1.373333,32.290275,800
Uganda,UGA,2011,149.4917134,24.28887594,1.373333,32.290275,800
Uganda,UGA,2012,145.7933214,26.03780047,1.373333,32.290275,800
Uganda,UGA,2013,143.3994909,28.21773339,1.373333,32.290275,800
Uganda,UGA,2014,140.2853872,29.54373347,1.373333,32.290275,800
Uganda,UGA,2015,136.256827,29.91523824,1.373333,32.290275,800
Uganda,UGA,2016,134.3820467,29.13120412,1.373333,32.290275,800
Uganda,UGA,2017,129.8468938,28.00674294,1.373333,32.290275,800
Uganda,UGA,2018,128.0926436,28.36923343,1.373333,32.290275,800
Uganda,UGA,2019,125.3390259,28.1217511,1.373333,32.290275,800
Ukraine,UKR,1990,13.27381521,86.6429962,48.379433,31.16558,804
Ukraine,UKR,1991,13.21329291,90.55687606,48.379433,31.16558,804
Ukraine,UKR,1992,13.17006917,94.18514522,48.379433,31.16558,804
Ukraine,UKR,1993,13.24765255,98.25531131,48.379433,31.16558,804
Ukraine,UKR,1994,13.21552798,101.1205801,48.379433,31.16558,804
Ukraine,UKR,1995,13.48087794,106.1153131,48.379433,31.16558,804
Ukraine,UKR,1996,12.93877411,102.4645039,48.379433,31.16558,804
Ukraine,UKR,1997,12.35170378,97.28603927,48.379433,31.16558,804
Ukraine,UKR,1998,11.52547302,90.12275896,48.379433,31.16558,804
Ukraine,UKR,1999,11.61005512,90.90519031,48.379433,31.16558,804
Ukraine,UKR,2000,11.57570707,91.82698061,48.379433,31.16558,804
Ukraine,UKR,2001,11.00554054,89.53554672,48.379433,31.16558,804
Ukraine,UKR,2002,10.69739246,90.46925547,48.379433,31.16558,804
Ukraine,UKR,2003,10.18436406,89.78553796,48.379433,31.16558,804
Ukraine,UKR,2004,9.741496464,90.33543872,48.379433,31.16558,804
Ukraine,UKR,2005,9.292509665,90.58037065,48.379433,31.16558,804
Ukraine,UKR,2006,8.32548579,86.19142388,48.379433,31.16558,804
Ukraine,UKR,2007,7.840077873,87.29974622,48.379433,31.16558,804
Ukraine,UKR,2008,7.214210662,86.90734027,48.379433,31.16558,804
Ukraine,UKR,2009,6.106862257,78.77185857,48.379433,31.16558,804
Ukraine,UKR,2010,5.528442014,75.68683781,48.379433,31.16558,804
Ukraine,UKR,2011,4.989190441,71.36816998,48.379433,31.16558,804
Ukraine,UKR,2012,4.692630946,69.2225679,48.379433,31.16558,804
Ukraine,UKR,2013,4.412550072,66.48250178,48.379433,31.16558,804
Ukraine,UKR,2014,3.94340812,60.14460987,48.379433,31.16558,804
Ukraine,UKR,2015,4.386978431,68.44136214,48.379433,31.16558,804
Ukraine,UKR,2016,4.040863506,60.89694921,48.379433,31.16558,804
Ukraine,UKR,2017,3.83446738,56.44219641,48.379433,31.16558,804
Ukraine,UKR,2018,3.767439484,57.6814704,48.379433,31.16558,804
Ukraine,UKR,2019,3.594425291,57.42673113,48.379433,31.16558,804
United Arab Emirates,ARE,1990,1.018377241,172.7619447,23.424076,53.847818,784
United Arab Emirates,ARE,1991,0.847869344,174.1931273,23.424076,53.847818,784
United Arab Emirates,ARE,1992,0.691579819,176.2752869,23.424076,53.847818,784
United Arab Emirates,ARE,1993,0.553275523,178.5535467,23.424076,53.847818,784
United Arab Emirates,ARE,1994,0.456425734,188.0054844,23.424076,53.847818,784
United Arab Emirates,ARE,1995,0.363361485,188.3593271,23.424076,53.847818,784
United Arab Emirates,ARE,1996,0.295132923,189.1871622,23.424076,53.847818,784
United Arab Emirates,ARE,1997,0.235641444,189.2739163,23.424076,53.847818,784
United Arab Emirates,ARE,1998,0.183967844,187.3016083,23.424076,53.847818,784
United Arab Emirates,ARE,1999,0.144213846,186.4724832,23.424076,53.847818,784
United Arab Emirates,ARE,2000,0.117734231,191.0570045,23.424076,53.847818,784
United Arab Emirates,ARE,2001,0.094787722,187.5233338,23.424076,53.847818,784
United Arab Emirates,ARE,2002,0.075579657,183.5956617,23.424076,53.847818,784
United Arab Emirates,ARE,2003,0.063126281,186.7048313,23.424076,53.847818,784
United Arab Emirates,ARE,2004,0.054500916,195.3451614,23.424076,53.847818,784
United Arab Emirates,ARE,2005,0.044157968,193.0577388,23.424076,53.847818,784
United Arab Emirates,ARE,2006,0.035153355,186.5028444,23.424076,53.847818,784
United Arab Emirates,ARE,2007,0.026523331,174.2077389,23.424076,53.847818,784
United Arab Emirates,ARE,2008,0.020287183,167.7497676,23.424076,53.847818,784
United Arab Emirates,ARE,2009,0.015934927,162.7022723,23.424076,53.847818,784
United Arab Emirates,ARE,2010,0.013133729,156.304743,23.424076,53.847818,784
United Arab Emirates,ARE,2011,0.011520369,151.859251,23.424076,53.847818,784
United Arab Emirates,ARE,2012,0.010302717,149.1138429,23.424076,53.847818,784
United Arab Emirates,ARE,2013,0.008842013,140.6151895,23.424076,53.847818,784
United Arab Emirates,ARE,2014,0.006626513,118.5221951,23.424076,53.847818,784
United Arab Emirates,ARE,2015,0.006155213,116.751414,23.424076,53.847818,784
United Arab Emirates,ARE,2016,0.005738425,113.1839453,23.424076,53.847818,784
United Arab Emirates,ARE,2017,0.005355563,109.8922776,23.424076,53.847818,784
United Arab Emirates,ARE,2018,0.004888505,107.0147293,23.424076,53.847818,784
United Arab Emirates,ARE,2019,0.004377592,104.9111961,23.424076,53.847818,784
United Kingdom,GBR,1990,0.087424432,45.94552323,55.378051,-3.435973,826
United Kingdom,GBR,1991,0.079950097,44.45414897,55.378051,-3.435973,826
United Kingdom,GBR,1992,0.073052162,42.74254522,55.378051,-3.435973,826
United Kingdom,GBR,1993,0.067797538,41.84191033,55.378051,-3.435973,826
United Kingdom,GBR,1994,0.061040138,39.65338195,55.378051,-3.435973,826
United Kingdom,GBR,1995,0.056399293,38.47102356,55.378051,-3.435973,826
United Kingdom,GBR,1996,0.051677729,36.67715727,55.378051,-3.435973,826
United Kingdom,GBR,1997,0.047179468,34.67436762,55.378051,-3.435973,826
United Kingdom,GBR,1998,0.043497655,33.1699136,55.378051,-3.435973,826
United Kingdom,GBR,1999,0.040166752,31.61673372,55.378051,-3.435973,826
United Kingdom,GBR,2000,0.036172925,29.4402116,55.378051,-3.435973,826
United Kingdom,GBR,2001,0.032781114,27.40523125,55.378051,-3.435973,826
United Kingdom,GBR,2002,0.030494279,26.3097976,55.378051,-3.435973,826
United Kingdom,GBR,2003,0.028209362,24.93278434,55.378051,-3.435973,826
United Kingdom,GBR,2004,0.025445842,22.99724795,55.378051,-3.435973,826
United Kingdom,GBR,2005,0.023238231,21.54400819,55.378051,-3.435973,826
United Kingdom,GBR,2006,0.021359627,20.31641076,55.378051,-3.435973,826
United Kingdom,GBR,2007,0.019790135,19.38647993,55.378051,-3.435973,826
United Kingdom,GBR,2008,0.018432491,18.38167861,55.378051,-3.435973,826
United Kingdom,GBR,2009,0.016831055,17.2362522,55.378051,-3.435973,826
United Kingdom,GBR,2010,0.015504992,16.25216456,55.378051,-3.435973,826
United Kingdom,GBR,2011,0.014255782,15.22577362,55.378051,-3.435973,826
United Kingdom,GBR,2012,0.013168787,14.35824917,55.378051,-3.435973,826
United Kingdom,GBR,2013,0.012156821,13.48497122,55.378051,-3.435973,826
United Kingdom,GBR,2014,0.011087507,12.54969577,55.378051,-3.435973,826
United Kingdom,GBR,2015,0.010432978,12.0050295,55.378051,-3.435973,826
United Kingdom,GBR,2016,0.009860971,11.6077413,55.378051,-3.435973,826
United Kingdom,GBR,2017,0.009381291,11.28303564,55.378051,-3.435973,826
United Kingdom,GBR,2018,0.009155637,11.45966154,55.378051,-3.435973,826
United Kingdom,GBR,2019,0.008776812,11.20859493,55.378051,-3.435973,826
United States of America,USA,1990,0.113357408,32.19690565,37.09024,-95.712891,840
United States of America,USA,1991,0.107610991,31.39503835,37.09024,-95.712891,840
United States of America,USA,1992,0.101671002,30.59836675,37.09024,-95.712891,840
United States of America,USA,1993,0.099394268,30.60880292,37.09024,-95.712891,840
United States of America,USA,1994,0.095366002,30.3016509,37.09024,-95.712891,840
United States of America,USA,1995,0.092606574,29.95375937,37.09024,-95.712891,840
United States of America,USA,1996,0.089735212,29.17915474,37.09024,-95.712891,840
United States of America,USA,1997,0.086863924,28.47779927,37.09024,-95.712891,840
United States of America,USA,1998,0.084753274,28.03276671,37.09024,-95.712891,840
United States of America,USA,1999,0.083260806,27.68163428,37.09024,-95.712891,840
United States of America,USA,2000,0.08059931,26.79645002,37.09024,-95.712891,840
United States of America,USA,2001,0.077279096,25.96548773,37.09024,-95.712891,840
United States of America,USA,2002,0.073969946,25.14877579,37.09024,-95.712891,840
United States of America,USA,2003,0.069813175,23.91589455,37.09024,-95.712891,840
United States of America,USA,2004,0.064707582,22.49778704,37.09024,-95.712891,840
United States of America,USA,2005,0.061343405,21.69653945,37.09024,-95.712891,840
United States of America,USA,2006,0.057263227,20.65581343,37.09024,-95.712891,840
United States of America,USA,2007,0.052913456,19.13357464,37.09024,-95.712891,840
United States of America,USA,2008,0.049235455,17.72925047,37.09024,-95.712891,840
United States of America,USA,2009,0.045427999,16.36447137,37.09024,-95.712891,840
United States of America,USA,2010,0.04189857,15.281863,37.09024,-95.712891,840
United States of America,USA,2011,0.039487424,14.86812614,37.09024,-95.712891,840
United States of America,USA,2012,0.037004206,14.07551314,37.09024,-95.712891,840
United States of America,USA,2013,0.034655847,13.32445951,37.09024,-95.712891,840
United States of America,USA,2014,0.032701327,12.52774204,37.09024,-95.712891,840
United States of America,USA,2015,0.030926163,12.00276413,37.09024,-95.712891,840
United States of America,USA,2016,0.029081096,11.32229611,37.09024,-95.712891,840
United States of America,USA,2017,0.027475051,10.69049717,37.09024,-95.712891,840
United States of America,USA,2018,0.027058935,10.64560782,37.09024,-95.712891,840
United States of America,USA,2019,0.026754245,10.60651482,37.09024,-95.712891,840
United States Virgin Islands,VIR,1990,3.598431825,21.84240455,18.335765,-64.896335,581
United States Virgin Islands,VIR,1991,3.200599479,21.25137128,18.335765,-64.896335,581
United States Virgin Islands,VIR,1992,2.890106108,21.04552373,18.335765,-64.896335,581
United States Virgin Islands,VIR,1993,2.636084175,20.93578394,18.335765,-64.896335,581
United States Virgin Islands,VIR,1994,2.436460177,21.00624597,18.335765,-64.896335,581
United States Virgin Islands,VIR,1995,2.19971346,20.32562713,18.335765,-64.896335,581
United States Virgin Islands,VIR,1996,2.045001416,19.97102634,18.335765,-64.896335,581
United States Virgin Islands,VIR,1997,1.886749389,19.13480876,18.335765,-64.896335,581
United States Virgin Islands,VIR,1998,1.754843549,18.26046832,18.335765,-64.896335,581
United States Virgin Islands,VIR,1999,1.658850102,17.73432249,18.335765,-64.896335,581
United States Virgin Islands,VIR,2000,1.538132903,16.97728278,18.335765,-64.896335,581
United States Virgin Islands,VIR,2001,1.419155236,16.42165377,18.335765,-64.896335,581
United States Virgin Islands,VIR,2002,1.283778984,15.50470834,18.335765,-64.896335,581
United States Virgin Islands,VIR,2003,1.165223581,14.7127151,18.335765,-64.896335,581
United States Virgin Islands,VIR,2004,1.061914814,13.92838482,18.335765,-64.896335,581
United States Virgin Islands,VIR,2005,0.972193403,13.5213978,18.335765,-64.896335,581
United States Virgin Islands,VIR,2006,0.912600498,13.78373807,18.335765,-64.896335,581
United States Virgin Islands,VIR,2007,0.92495508,15.66712704,18.335765,-64.896335,581
United States Virgin Islands,VIR,2008,0.853073067,15.89506947,18.335765,-64.896335,581
United States Virgin Islands,VIR,2009,0.787752949,16.05676323,18.335765,-64.896335,581
United States Virgin Islands,VIR,2010,0.734201254,16.2207296,18.335765,-64.896335,581
United States Virgin Islands,VIR,2011,0.687800565,16.4151445,18.335765,-64.896335,581
United States Virgin Islands,VIR,2012,0.646685856,16.68594809,18.335765,-64.896335,581
United States Virgin Islands,VIR,2013,0.608310648,16.9334622,18.335765,-64.896335,581
United States Virgin Islands,VIR,2014,0.57560967,17.1688993,18.335765,-64.896335,581
United States Virgin Islands,VIR,2015,0.550758096,17.42992278,18.335765,-64.896335,581
United States Virgin Islands,VIR,2016,0.522708752,17.31374463,18.335765,-64.896335,581
United States Virgin Islands,VIR,2017,0.505642376,17.41916516,18.335765,-64.896335,581
United States Virgin Islands,VIR,2018,0.487944737,17.59959481,18.335765,-64.896335,581
United States Virgin Islands,VIR,2019,0.470623893,17.81955389,18.335765,-64.896335,581
Uruguay,URY,1990,10.4993635,23.72909168,-32.522779,-55.765835,858
Uruguay,URY,1991,9.089402423,22.39009951,-32.522779,-55.765835,858
Uruguay,URY,1992,8.401076762,22.74058906,-32.522779,-55.765835,858
Uruguay,URY,1993,7.763705925,23.03760274,-32.522779,-55.765835,858
Uruguay,URY,1994,6.890489476,22.42783778,-32.522779,-55.765835,858
Uruguay,URY,1995,6.295486699,22.43076438,-32.522779,-55.765835,858
Uruguay,URY,1996,5.623976467,21.90274467,-32.522779,-55.765835,858
Uruguay,URY,1997,4.984406083,21.25465996,-32.522779,-55.765835,858
Uruguay,URY,1998,4.583321016,21.41991699,-32.522779,-55.765835,858
Uruguay,URY,1999,4.135702586,21.00111954,-32.522779,-55.765835,858
Uruguay,URY,2000,3.686370454,19.9137045,-32.522779,-55.765835,858
Uruguay,URY,2001,3.403876105,19.08186263,-32.522779,-55.765835,858
Uruguay,URY,2002,3.225553541,18.39528051,-32.522779,-55.765835,858
Uruguay,URY,2003,3.104348724,17.80846733,-32.522779,-55.765835,858
Uruguay,URY,2004,2.91791787,16.88492161,-32.522779,-55.765835,858
Uruguay,URY,2005,2.694156317,16.13630628,-32.522779,-55.765835,858
Uruguay,URY,2006,2.453098274,15.51299827,-32.522779,-55.765835,858
Uruguay,URY,2007,2.373375896,15.88210373,-32.522779,-55.765835,858
Uruguay,URY,2008,2.126212122,14.99801297,-32.522779,-55.765835,858
Uruguay,URY,2009,1.939672633,14.64179752,-32.522779,-55.765835,858
Uruguay,URY,2010,1.815957623,14.6176211,-32.522779,-55.765835,858
Uruguay,URY,2011,1.734723831,15.03705549,-32.522779,-55.765835,858
Uruguay,URY,2012,1.604753388,15.07723558,-32.522779,-55.765835,858
Uruguay,URY,2013,1.466267283,14.93548502,-32.522779,-55.765835,858
Uruguay,URY,2014,1.335229154,14.63352434,-32.522779,-55.765835,858
Uruguay,URY,2015,1.242621483,14.53793976,-32.522779,-55.765835,858
Uruguay,URY,2016,1.136863488,14.02956861,-32.522779,-55.765835,858
Uruguay,URY,2017,1.053122479,13.44092719,-32.522779,-55.765835,858
Uruguay,URY,2018,0.979502716,13.55299424,-32.522779,-55.765835,858
Uruguay,URY,2019,0.921390217,13.51287398,-32.522779,-55.765835,858
Uzbekistan,UZB,1990,67.17111613,81.05839324,41.377491,64.585262,860
Uzbekistan,UZB,1991,68.13539043,87.39154212,41.377491,64.585262,860
Uzbekistan,UZB,1992,70.92397585,96.45169844,41.377491,64.585262,860
Uzbekistan,UZB,1993,75.70641528,109.599615,41.377491,64.585262,860
Uzbekistan,UZB,1994,78.84603352,121.7761635,41.377491,64.585262,860
Uzbekistan,UZB,1995,79.22459485,130.4584019,41.377491,64.585262,860
Uzbekistan,UZB,1996,78.60587975,138.4497598,41.377491,64.585262,860
Uzbekistan,UZB,1997,75.30339657,142.2494004,41.377491,64.585262,860
Uzbekistan,UZB,1998,72.85818553,147.7672797,41.377491,64.585262,860
Uzbekistan,UZB,1999,69.74134071,151.4258788,41.377491,64.585262,860
Uzbekistan,UZB,2000,70.21912221,160.7551414,41.377491,64.585262,860
Uzbekistan,UZB,2001,70.02797546,165.3190084,41.377491,64.585262,860
Uzbekistan,UZB,2002,70.88994457,170.7187408,41.377491,64.585262,860
Uzbekistan,UZB,2003,71.55512304,175.4004585,41.377491,64.585262,860
Uzbekistan,UZB,2004,71.29341961,178.3421936,41.377491,64.585262,860
Uzbekistan,UZB,2005,71.46473624,185.0410448,41.377491,64.585262,860
Uzbekistan,UZB,2006,66.17914269,180.4078676,41.377491,64.585262,860
Uzbekistan,UZB,2007,61.05463621,178.7430977,41.377491,64.585262,860
Uzbekistan,UZB,2008,57.53252048,182.3073498,41.377491,64.585262,860
Uzbekistan,UZB,2009,53.08989801,182.8476129,41.377491,64.585262,860
Uzbekistan,UZB,2010,49.96629418,187.0381195,41.377491,64.585262,860
Uzbekistan,UZB,2011,47.19232486,193.659967,41.377491,64.585262,860
Uzbekistan,UZB,2012,43.80805748,199.3680326,41.377491,64.585262,860
Uzbekistan,UZB,2013,39.74887742,201.3671934,41.377491,64.585262,860
Uzbekistan,UZB,2014,35.99815675,202.2158999,41.377491,64.585262,860
Uzbekistan,UZB,2015,32.66501097,201.5279474,41.377491,64.585262,860
Uzbekistan,UZB,2016,29.21081545,195.9758998,41.377491,64.585262,860
Uzbekistan,UZB,2017,26.37265928,191.4447754,41.377491,64.585262,860
Uzbekistan,UZB,2018,23.82686423,185.8246599,41.377491,64.585262,860
Uzbekistan,UZB,2019,21.37508078,178.5158805,41.377491,64.585262,860
Vanuatu,VUT,1990,269.0475789,20.42448391,-15.376706,166.959158,548
Vanuatu,VUT,1991,272.4611927,21.68261675,-15.376706,166.959158,548
Vanuatu,VUT,1992,275.0030542,22.85587703,-15.376706,166.959158,548
Vanuatu,VUT,1993,275.3587969,23.81678708,-15.376706,166.959158,548
Vanuatu,VUT,1994,277.4639229,24.78209281,-15.376706,166.959158,548
Vanuatu,VUT,1995,272.5627243,25.07013062,-15.376706,166.959158,548
Vanuatu,VUT,1996,271.5562845,25.59158408,-15.376706,166.959158,548
Vanuatu,VUT,1997,268.7851349,25.99013674,-15.376706,166.959158,548
Vanuatu,VUT,1998,265.6444699,26.28152925,-15.376706,166.959158,548
Vanuatu,VUT,1999,264.4909432,26.63410965,-15.376706,166.959158,548
Vanuatu,VUT,2000,255.7643219,25.99126431,-15.376706,166.959158,548
Vanuatu,VUT,2001,254.0370582,25.99564355,-15.376706,166.959158,548
Vanuatu,VUT,2002,243.2867369,25.09028022,-15.376706,166.959158,548
Vanuatu,VUT,2003,235.3817981,24.47544765,-15.376706,166.959158,548
Vanuatu,VUT,2004,233.0526865,24.46829538,-15.376706,166.959158,548
Vanuatu,VUT,2005,236.5758452,25.0352281,-15.376706,166.959158,548
Vanuatu,VUT,2006,236.8046932,25.74715394,-15.376706,166.959158,548
Vanuatu,VUT,2007,238.1333756,26.89094804,-15.376706,166.959158,548
Vanuatu,VUT,2008,238.0364227,28.14101859,-15.376706,166.959158,548
Vanuatu,VUT,2009,235.9104515,29.03243611,-15.376706,166.959158,548
Vanuatu,VUT,2010,234.0272397,29.48651234,-15.376706,166.959158,548
Vanuatu,VUT,2011,235.2919162,30.03381769,-15.376706,166.959158,548
Vanuatu,VUT,2012,233.8976916,30.22231781,-15.376706,166.959158,548
Vanuatu,VUT,2013,232.8269383,30.41100664,-15.376706,166.959158,548
Vanuatu,VUT,2014,231.3940789,30.57245074,-15.376706,166.959158,548
Vanuatu,VUT,2015,229.4428367,30.68673819,-15.376706,166.959158,548
Vanuatu,VUT,2016,226.9903804,31.44534098,-15.376706,166.959158,548
Vanuatu,VUT,2017,223.8356817,31.97560082,-15.376706,166.959158,548
Vanuatu,VUT,2018,220.9685085,32.83247173,-15.376706,166.959158,548
Vanuatu,VUT,2019,217.726538,33.21905863,-15.376706,166.959158,548
Venezuela,VEN,1990,3.718317272,48.5514547,6.42375,-66.58973,862
Venezuela,VEN,1991,3.363723088,48.08657496,6.42375,-66.58973,862
Venezuela,VEN,1992,3.051519105,47.73548562,6.42375,-66.58973,862
Venezuela,VEN,1993,2.764535408,47.59659333,6.42375,-66.58973,862
Venezuela,VEN,1994,2.626942791,49.17835076,6.42375,-66.58973,862
Venezuela,VEN,1995,2.395028949,48.29062128,6.42375,-66.58973,862
Venezuela,VEN,1996,2.14650203,46.21681518,6.42375,-66.58973,862
Venezuela,VEN,1997,1.928297046,44.41333083,6.42375,-66.58973,862
Venezuela,VEN,1998,1.837193899,45.62893947,6.42375,-66.58973,862
Venezuela,VEN,1999,1.731785002,45.71563002,6.42375,-66.58973,862
Venezuela,VEN,2000,1.603257905,44.92700889,6.42375,-66.58973,862
Venezuela,VEN,2001,1.525557102,45.06200098,6.42375,-66.58973,862
Venezuela,VEN,2002,1.47984548,45.56862438,6.42375,-66.58973,862
Venezuela,VEN,2003,1.432976278,46.5097233,6.42375,-66.58973,862
Venezuela,VEN,2004,1.26655369,42.94829725,6.42375,-66.58973,862
Venezuela,VEN,2005,1.173121202,42.34471652,6.42375,-66.58973,862
Venezuela,VEN,2006,1.092266235,43.95137844,6.42375,-66.58973,862
Venezuela,VEN,2007,0.977876773,45.60694459,6.42375,-66.58973,862
Venezuela,VEN,2008,0.86315874,47.65780906,6.42375,-66.58973,862
Venezuela,VEN,2009,0.732850493,47.7918049,6.42375,-66.58973,862
Venezuela,VEN,2010,0.609544517,44.94588877,6.42375,-66.58973,862
Venezuela,VEN,2011,0.546873338,44.5936535,6.42375,-66.58973,862
Venezuela,VEN,2012,0.496001162,44.8179082,6.42375,-66.58973,862
Venezuela,VEN,2013,0.437791235,43.09097135,6.42375,-66.58973,862
Venezuela,VEN,2014,0.40299785,42.36581239,6.42375,-66.58973,862
Venezuela,VEN,2015,0.370361428,41.71125193,6.42375,-66.58973,862
Venezuela,VEN,2016,0.353023552,41.75087264,6.42375,-66.58973,862
Venezuela,VEN,2017,0.336940793,41.69878506,6.42375,-66.58973,862
Venezuela,VEN,2018,0.318644091,42.24828564,6.42375,-66.58973,862
Venezuela,VEN,2019,0.313694005,44.79351803,6.42375,-66.58973,862
Vietnam,VNM,1990,152.807841,25.49948426,14.058324,108.277199,704
Vietnam,VNM,1991,148.4890119,26.17216734,14.058324,108.277199,704
Vietnam,VNM,1992,143.830983,26.88184497,14.058324,108.277199,704
Vietnam,VNM,1993,139.0722145,27.62254445,14.058324,108.277199,704
Vietnam,VNM,1994,134.2715041,28.42151844,14.058324,108.277199,704
Vietnam,VNM,1995,129.6114801,29.2881604,14.058324,108.277199,704
Vietnam,VNM,1996,124.838248,30.11836407,14.058324,108.277199,704
Vietnam,VNM,1997,120.0777088,31.28930804,14.058324,108.277199,704
Vietnam,VNM,1998,115.3020891,32.32975329,14.058324,108.277199,704
Vietnam,VNM,1999,110.7644177,33.50803957,14.058324,108.277199,704
Vietnam,VNM,2000,106.5211928,34.61371126,14.058324,108.277199,704
Vietnam,VNM,2001,102.7215184,36.34782707,14.058324,108.277199,704
Vietnam,VNM,2002,98.82587391,38.36802417,14.058324,108.277199,704
Vietnam,VNM,2003,95.05864825,40.91057028,14.058324,108.277199,704
Vietnam,VNM,2004,91.3746185,42.98246043,14.058324,108.277199,704
Vietnam,VNM,2005,87.60476397,44.84171299,14.058324,108.277199,704
Vietnam,VNM,2006,83.51011094,46.57706533,14.058324,108.277199,704
Vietnam,VNM,2007,79.51224143,49.16240399,14.058324,108.277199,704
Vietnam,VNM,2008,75.45673789,51.42886386,14.058324,108.277199,704
Vietnam,VNM,2009,71.51447927,52.88073805,14.058324,108.277199,704
Vietnam,VNM,2010,67.64257683,53.47005038,14.058324,108.277199,704
Vietnam,VNM,2011,64.17836331,53.17877201,14.058324,108.277199,704
Vietnam,VNM,2012,60.87978179,52.18099636,14.058324,108.277199,704
Vietnam,VNM,2013,57.81784242,50.6421009,14.058324,108.277199,704
Vietnam,VNM,2014,54.80380525,49.15869818,14.058324,108.277199,704
Vietnam,VNM,2015,51.80617479,48.09189898,14.058324,108.277199,704
Vietnam,VNM,2016,48.88091018,47.00663095,14.058324,108.277199,704
Vietnam,VNM,2017,46.06272039,46.09250349,14.058324,108.277199,704
Vietnam,VNM,2018,43.24783187,46.16267634,14.058324,108.277199,704
Vietnam,VNM,2019,40.38293701,46.56455207,14.058324,108.277199,704
Yemen,YEM,1990,253.1840764,31.48566927,15.552727,48.516388,887
Yemen,YEM,1991,246.0336482,31.20648653,15.552727,48.516388,887
Yemen,YEM,1992,239.0758321,31.49327829,15.552727,48.516388,887
Yemen,YEM,1993,231.7909279,32.20611342,15.552727,48.516388,887
Yemen,YEM,1994,224.2831401,33.20915814,15.552727,48.516388,887
Yemen,YEM,1995,216.3894972,34.34103805,15.552727,48.516388,887
Yemen,YEM,1996,207.262277,36.09802185,15.552727,48.516388,887
Yemen,YEM,1997,197.4785373,39.30896567,15.552727,48.516388,887
Yemen,YEM,1998,186.5864638,42.83164738,15.552727,48.516388,887
Yemen,YEM,1999,177.3391111,46.81941059,15.552727,48.516388,887
Yemen,YEM,2000,168.1245013,49.34543276,15.552727,48.516388,887
Yemen,YEM,2001,158.8148871,50.70366593,15.552727,48.516388,887
Yemen,YEM,2002,151.2402284,52.02797018,15.552727,48.516388,887
Yemen,YEM,2003,143.2889514,53.2723448,15.552727,48.516388,887
Yemen,YEM,2004,135.9701277,54.54852751,15.552727,48.516388,887
Yemen,YEM,2005,129.0017393,56.17910659,15.552727,48.516388,887
Yemen,YEM,2006,122.9019014,58.4442382,15.552727,48.516388,887
Yemen,YEM,2007,117.1051631,60.98102938,15.552727,48.516388,887
Yemen,YEM,2008,112.1747158,63.69882022,15.552727,48.516388,887
Yemen,YEM,2009,106.4054281,65.65047713,15.552727,48.516388,887
Yemen,YEM,2010,100.4205185,67.40557944,15.552727,48.516388,887
Yemen,YEM,2011,96.17899747,70.51327188,15.552727,48.516388,887
Yemen,YEM,2012,91.76766926,73.63423767,15.552727,48.516388,887
Yemen,YEM,2013,87.7094321,76.71059566,15.552727,48.516388,887
Yemen,YEM,2014,83.44202023,78.6280617,15.552727,48.516388,887
Yemen,YEM,2015,80.6306723,80.94293065,15.552727,48.516388,887
Yemen,YEM,2016,77.63474198,81.68969811,15.552727,48.516388,887
Yemen,YEM,2017,75.22890476,82.92632632,15.552727,48.516388,887
Yemen,YEM,2018,72.67673055,84.50588152,15.552727,48.516388,887
Yemen,YEM,2019,69.57654809,85.61756938,15.552727,48.516388,887
Zambia,ZMB,1990,214.92761,21.78178812,-13.133897,27.849332,894
Zambia,ZMB,1991,216.6051027,22.33800978,-13.133897,27.849332,894
Zambia,ZMB,1992,216.8438661,22.42030728,-13.133897,27.849332,894
Zambia,ZMB,1993,216.0072784,22.6020219,-13.133897,27.849332,894
Zambia,ZMB,1994,215.8177705,22.77289847,-13.133897,27.849332,894
Zambia,ZMB,1995,215.8033798,23.40415382,-13.133897,27.849332,894
Zambia,ZMB,1996,214.5940183,24.03014416,-13.133897,27.849332,894
Zambia,ZMB,1997,212.1144482,25.00491138,-13.133897,27.849332,894
Zambia,ZMB,1998,209.5141225,25.74963953,-13.133897,27.849332,894
Zambia,ZMB,1999,206.2074599,26.4823527,-13.133897,27.849332,894
Zambia,ZMB,2000,203.4253126,26.60880594,-13.133897,27.849332,894
Zambia,ZMB,2001,199.3854666,26.79766413,-13.133897,27.849332,894
Zambia,ZMB,2002,196.0932278,26.78333302,-13.133897,27.849332,894
Zambia,ZMB,2003,193.4224525,26.98447117,-13.133897,27.849332,894
Zambia,ZMB,2004,190.8611413,27.87075367,-13.133897,27.849332,894
Zambia,ZMB,2005,187.0260439,28.94362608,-13.133897,27.849332,894
Zambia,ZMB,2006,183.1985842,30.72199141,-13.133897,27.849332,894
Zambia,ZMB,2007,175.8085544,31.24599744,-13.133897,27.849332,894
Zambia,ZMB,2008,168.6879029,31.70309525,-13.133897,27.849332,894
Zambia,ZMB,2009,161.0447413,32.04893766,-13.133897,27.849332,894
Zambia,ZMB,2010,156.2052452,33.30601157,-13.133897,27.849332,894
Zambia,ZMB,2011,151.341678,34.97725351,-13.133897,27.849332,894
Zambia,ZMB,2012,144.8010963,36.48242859,-13.133897,27.849332,894
Zambia,ZMB,2013,138.4705456,37.83773037,-13.133897,27.849332,894
Zambia,ZMB,2014,132.840087,38.72406087,-13.133897,27.849332,894
Zambia,ZMB,2015,128.4058119,39.234528,-13.133897,27.849332,894
Zambia,ZMB,2016,124.4322703,39.50074881,-13.133897,27.849332,894
Zambia,ZMB,2017,120.360473,39.71652205,-13.133897,27.849332,894
Zambia,ZMB,2018,115.825765,39.87298343,-13.133897,27.849332,894
Zambia,ZMB,2019,111.1066299,40.60824797,-13.133897,27.849332,894
Zimbabwe,ZWE,1990,144.2169563,25.39293992,-19.015438,29.154857,716
Zimbabwe,ZWE,1991,137.9810819,25.65652671,-19.015438,29.154857,716
Zimbabwe,ZWE,1992,134.9789714,26.38283883,-19.015438,29.154857,716
Zimbabwe,ZWE,1993,130.0289109,26.76923049,-19.015438,29.154857,716
Zimbabwe,ZWE,1994,125.8936395,27.34059638,-19.015438,29.154857,716
Zimbabwe,ZWE,1995,123.0876513,28.319945,-19.015438,29.154857,716
Zimbabwe,ZWE,1996,117.8484747,28.76515828,-19.015438,29.154857,716
Zimbabwe,ZWE,1997,114.6482885,29.79484867,-19.015438,29.154857,716
Zimbabwe,ZWE,1998,116.1544486,31.56153851,-19.015438,29.154857,716
Zimbabwe,ZWE,1999,119.0781159,33.36302392,-19.015438,29.154857,716
Zimbabwe,ZWE,2000,124.6527209,35.04683809,-19.015438,29.154857,716
Zimbabwe,ZWE,2001,126.7047257,35.36373026,-19.015438,29.154857,716
Zimbabwe,ZWE,2002,131.1658737,35.9116718,-19.015438,29.154857,716
Zimbabwe,ZWE,2003,134.786976,36.12332184,-19.015438,29.154857,716
Zimbabwe,ZWE,2004,139.7634465,36.88286667,-19.015438,29.154857,716
Zimbabwe,ZWE,2005,141.7363346,37.12930955,-19.015438,29.154857,716
Zimbabwe,ZWE,2006,146.0277706,37.82637226,-19.015438,29.154857,716
Zimbabwe,ZWE,2007,151.114884,37.67678095,-19.015438,29.154857,716
Zimbabwe,ZWE,2008,159.9419857,38.06681511,-19.015438,29.154857,716
Zimbabwe,ZWE,2009,164.4966339,37.54379588,-19.015438,29.154857,716
Zimbabwe,ZWE,2010,164.7942302,37.12222049,-19.015438,29.154857,716
Zimbabwe,ZWE,2011,160.7583517,37.19593836,-19.015438,29.154857,716
Zimbabwe,ZWE,2012,155.4179408,38.02362996,-19.015438,29.154857,716
Zimbabwe,ZWE,2013,149.8343516,38.98127655,-19.015438,29.154857,716
Zimbabwe,ZWE,2014,146.341096,39.8305529,-19.015438,29.154857,716
Zimbabwe,ZWE,2015,143.4779572,40.08806216,-19.015438,29.154857,716
Zimbabwe,ZWE,2016,140.6432453,38.81753778,-19.015438,29.154857,716
Zimbabwe,ZWE,2017,137.448374,37.25858069,-19.015438,29.154857,716
Zimbabwe,ZWE,2018,133.9230307,36.34021346,-19.015438,29.154857,716
Zimbabwe,ZWE,2019,130.508301,35.84053238,-19.015438,29.154857,716"""
        |> fromCSV
```