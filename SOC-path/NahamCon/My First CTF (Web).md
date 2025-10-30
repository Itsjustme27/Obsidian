
# NahamCon 2025 CTF Web Challenge: "Nz Gjstu DUG" (Am Twist PNG)

## Challenge Recap

- **Webpage**: Shows a centered `rotten.jpg` and a repeating background `bg.png`.
    
- **Hint**: Title is ROT13 for "Nz Gjstu DUG" is "Am Twist PNG" — suggests a PNG stego challenge with a twist.
    
- **zsteg Output**: Reveals long, encoded-looking strings in blue channel, 7th bit, at prime coordinates.

#### z-steg output:

```bash
zsteg -a bg.png       
meta XML:com.adobe.xmp.. text: "<x:xmpmeta xmlns:x=\"adobe:ns:meta/\" x:xmptk=\"XMP Core 6.0.0\">\n   <rdf:RDF xmlns:rdf=\"http://www.w3.org/1999/02/22-rdf-syntax-ns#\">\n      <rdf:Description rdf:about=\"\"\n            xmlns:exif=\"http://ns.adobe.com/exif/1.0/\">\n         <exif:PixelYDimension>210</exif:PixelYDimension>\n         <exif:PixelXDimension>226</exif:PixelXDimension>\n         <exif:UserComment>Screenshot</exif:UserComment>\n      </rdf:Description>\n   </rdf:RDF>\n</x:xmpmeta>\n"
imagedata           .. file: AIX core file fulldump 32-bit, \001
b1,b,lsb,xy         .. text: "+6R8}e_1"
b2,g,lsb,xy         .. text: "b#.tP;5:"
b2,g,msb,xy         .. file: OpenPGP Secret Key
b3,b,msb,xy         .. file: OpenPGP Public Key
b3,rgb,lsb,xy       .. text: "c1u(\\3N1T"
b3p,r,lsb,xy        .. text: "owFoBjpk"
b3p,rgb,lsb,xy      .. text: "zQ,,((KEJPy~"
b4,r,lsb,xy         .. text: "T\"#4Wt33\"5eCEfB"
b4,r,msb,xy         .. text: "HD,jf*,\"\"*"
b4,rgba,lsb,xy      .. text: "_=OMO<_,o"
b5p,r,msb,xy        .. text: "QI9um59%%5"
b5p,abgr,lsb,xy     .. file: AIX core file
b6,r,msb,xy         .. file: SYMMETRY i386 executable (invalid @ 0)
b6p,g,lsb,xy        .. text: "xojih{gs"
b6p,abgr,lsb,xy     .. file: AIX core file
b7p,b,lsb,xy        .. text: "vlont|smov"
b7p,bgr,lsb,xy      .. text: "wplmoooqu}}xromnorv|"
b7p,abgr,lsb,xy     .. file: AIX core file 64-bit, \373
b8,r,msb,xy         .. text: "/o//ooo/OO"
b1,rgba,lsb,xy,prime.. text: ";5S1S9}Y{="
b2,g,lsb,xy,prime   .. file: OpenPGP Secret Key
b2,b,lsb,xy,prime   .. text: "A&ZJ%1\\{"
b3,r,lsb,xy,prime   .. text: "i^BrI`nf"
b3,r,msb,xy,prime   .. text: "ZTFTo*Wa"
b3,bgr,lsb,xy,prime .. text: "b5x{lHuMf"
b3,bgr,msb,xy,prime .. file: OpenPGP Public Key
b3,rgba,lsb,xy,prime.. text: "zgMz_|w/"
b4,r,lsb,xy,prime   .. text: "PF@U#72Ftet3!$@R!F"
b4,abgr,msb,xy,prime.. text: "oC?(_'O\t"
b5,r,lsb,xy,prime   .. file: OpenPGP Secret Key
b5,rgb,lsb,xy,prime .. file: OpenPGP Secret Key
b5,rgba,lsb,xy,prime.. file: OpenPGP Secret Key
b5p,rgb,lsb,xy,prime.. file: OpenPGP Secret Key
b5p,abgr,msb,xy,prime.. file: RDI Acoustic Doppler Current Profiler (ADCP)
b6,bgr,msb,xy,prime .. file: OpenPGP Public Key
b6p,g,lsb,xy,prime  .. text: "wvo~xtws}"
b6p,abgr,msb,xy,prime.. file: RDI Acoustic Doppler Current Profiler (ADCP)
b7p,b,lsb,xy,prime  .. text: "lnyrukqlovt{ooqsxhprp|{ypnlt{jwfpeqtoezkqk{t}nnn{ywv|njrtvu"
b7p,bgr,lsb,xy,prime.. text: "lmoqxor|usjkqwlinjvutqzoozncqzrcxqhup}rlpy}q{wysqpnmlyteznkiw{fxqyewqju`nber{qjkqvkfzvuq}rounpoizzxwvfwu}lnpjistutw|uw"
b7p,abgr,msb,xy,prime.. file: RDI Acoustic Doppler Current Profiler (ADCP)
b8,r,msb,xy,prime   .. text: "/O/Oo7/wO"
b8,abgr,msb,xy,prime.. file: very old 16-bit-int big-endian archive
b3p,b,lsb,yx        .. text: "`sQYgh+jq"
b3p,rgb,lsb,yx      .. text: "x\\XXWR1["
b4,r,lsb,yx         .. text: "feCEDfDvB"
b4,bgr,msb,yx       .. text: " O~lMbG2"
b4,abgr,msb,yx      .. text: "_ _/_h_h"
b5p,b,msb,yx        .. file: OpenPGP Public Key
b5p,rgb,msb,yx      .. text: "iMUUMeAA)i"
b5p,bgr,msb,yx      .. text: "}[G[K}II5m"
b6,r,msb,yx         .. file: SYMMETRY i386 executable (invalid @ 0) not stripped
b6p,g,lsb,yx        .. text: "|jxcgvxt"
b6p,g,msb,yx        .. file: MySQL table definition file Version 33, MySQL version -31362802
b6p,rgb,msb,yx      .. text: "S[kk[KCC"
b6p,bgr,msb,yx      .. text: "{wOwW{SS+["
b6p,abgr,lsb,yx     .. file: MPEG ADTS, layer II, v1, Monaural
b7p,b,lsb,yx        .. text: "wswpuwropunntlsprpjtovuqtnvqsnenbblqotohlmx|rqtts~vixwxrrm"
b7p,bgr,lsb,yx      .. text: "wsrvwrpqtwvvsqonpttrnhnytpmlsrqpsupikttqnowyurqsuqotwqqssooldfnlbacimppnontxnghmlllry}}xrpqrtuuusv~}vlhrytwzyusqrpmw"
b8,g,msb,yx         .. text: "{GGGG{[[;{"
b1,b,msb,yx,prime   .. file: OpenPGP Secret Key
b1,bgr,lsb,yx,prime .. text: "GOVf`M{^R]"
b2,r,msb,yx,prime   .. text: "k7xq)_f(}ntT"
b4,r,lsb,yx,prime   .. text: "3?CQ53&R"
b4,r,msb,yx,prime   .. text: "&,\"\"L\"J\""
b4,b,lsb,yx,prime   .. file: OpenPGP Public Key
b4,rgb,msb,yx,prime .. text: "%PB+_|Acr)"
b4,bgr,msb,yx,prime .. text: "R KR/qlCy"
b5,g,lsb,yx,prime   .. file: raw G3 (Group 3) FAX, byte-padded
b5,rgb,lsb,yx,prime .. file: OpenPGP Public Key
b5,rgba,lsb,yx,prime.. file: OpenPGP Public Key
b5p,r,lsb,yx,prime  .. file: OpenPGP Public Key
b5p,r,msb,yx,prime  .. text: "-9%%Y%U%"
b5p,g,lsb,yx,prime  .. file: TTComp archive data, binary, 2K dictionary
b5p,rgb,lsb,yx,prime.. file: OpenPGP Public Key
b6p,g,lsb,yx,prime  .. text: "|yuxr{{y}"
b7p,b,lsb,yx,prime  .. text: "srvuypnrminrvstV|vxsnvwqswknnqtvnw|ltzpr{w}tce~wmirhtxrowpugjbqtmuhykyrowwswpnsi||uq}{y}qvwqqotkpnlw{lmwwusvpwxounjlnspynwsflqrmpyhloxtxvksppuchirxsupcpgu|qnqpw^upzejrjxmrnq_tofuusdu_upw`ynvxnq\\k{cqlmtyqizozu_{maqwbxrzqrlzkoytipplqwatjqyjqquzrpxhokm|jssmyn"
b7p,bgr,lsb,yx,prime.. text: "rvrqvqtryrptoysqlfinnmrpvlrzupVd|}vyxxsrotvivnqor{vrkjntoipktpwloxw^|}mtutzuplrqzovr}ruqbrev~avslohosxhtttxxrunowrptuvfrjpbxqbuimfusi}ysjrxvsqoswgwzs_wspeomrghz}q}ttjpr|jzrxo}bqrvuvwqfpwosttjjpuniluwkzom|l{wnw{tvrfwupmvfxhnvtwoxjqlxntrsp|yvoyvvrvfimlpnrhlw"
b3,g,msb,XY         .. file: OpenPGP Secret Key
b3,b,msb,XY         .. file: OpenPGP Secret Key
b3p,rgb,lsb,XY      .. text: "mL{{vw(*"
b3p,bgr,lsb,XY      .. text: "I$m!di)m"
b4,r,lsb,XY         .. text: "#C\"GuUCC"
b4,bgr,lsb,XY       .. text: "n<6~?}}>8"
b5,r,lsb,XY         .. file: OpenPGP Secret Key
b5,rgb,lsb,XY       .. file: OpenPGP Secret Key
b5,rgba,lsb,XY      .. file: OpenPGP Secret Key
b6p,g,lsb,XY        .. text: "nmLXMt{{w"
b7p,b,lsb,XY        .. text: "jfSYWilony{obvujpbklptowvyttgpbpnullspyyhyquqq{ko\\Z]jwsnjpwwpsqyuuinnUgwsZ^XVhkxko"
b7p,bgr,lsb,XY      .. text: "kdgaSRXVWciflyn_o}xw{wogblwxtkkpqlcaknmmpttqnrvvvtyzuqupgkqicmpmnutrlimqrsptyzxjiyxrqouvpopv{sjoof]X[a\\^kuvwrnoljlqtwvvrqpssprywtwtkinnmohTSgrwvrgZ]^]YQWahlkoyujjnz"
b2,r,lsb,XY,prime   .. file: OpenPGP Public Key
b3,g,lsb,XY,prime   .. text: "Cb8A8us|"
b4,r,lsb,XY,prime   .. text: "W35Q`UUT#P]55BF?="
b5,r,lsb,XY,prime   .. file: OpenPGP Secret Key
b5,rgb,lsb,XY,prime .. file: OpenPGP Secret Key
b5,rgb,msb,XY,prime .. text: "l1&s?rX)"
b5,rgba,lsb,XY,prime.. file: OpenPGP Secret Key
b5p,g,msb,XY,prime  .. file: OpenPGP Public Key
b5p,b,lsb,XY,prime  .. file: OpenPGP Public Key
b5p,bgr,lsb,XY,prime.. file: OpenPGP Public Key
b6p,g,lsb,XY,prime  .. text: "qyl{{uzp|pk"
b6p,rgb,msb,XY,prime.. text: "s[CC=M{]"
b6p,abgr,lsb,XY,prime.. file: MPEG ADTS, layer II, v1, Monaural
b7p,b,lsb,XY,prime  .. text: "fSf}gqtvhrssf_nwi\\oh|qwuhN]stpqzrspmyuqtruttOdiuyl_xsiexuwmvq{"
b7p,bgr,lsb,XY,prime.. text: "gaRVfy}wgkpntqvqimrqsjrofa^wnlwkhS]Qozil}}qowntnh`N|\\rswuuquqozhstrsqumnybtbqvuurquvtatXOfdpigtoxwmt^jyusniveVyiuzwrlswupo{f"
b1,bgr,msb,YX       .. text: "H&82tA;{8"
b2,g,lsb,YX         .. text: "T%#FQQXN"
b3,r,lsb,YX         .. text: "cnI#nY$l"
b3,b,msb,YX         .. text: "8v1pgZnm"
b3,bgr,lsb,YX       .. text: "fhs#4+X\t"
b3p,r,msb,YX        .. text: "nM4q\n]\r1"
b3p,rgb,lsb,YX      .. text: "}VU[~`b}"
b3p,bgr,lsb,YX      .. text: "\\|66\\CB?<FF "
b4,r,lsb,YX         .. text: "D\"C#Fd3C"
b5,r,lsb,YX         .. file: OpenPGP Secret Key
b5,rgb,lsb,YX       .. file: OpenPGP Secret Key
b5,rgba,lsb,YX      .. file: OpenPGP Secret Key
b6p,r,lsb,YX        .. file: AVR firmware, reset at 0x00c9
b6p,g,lsb,YX        .. text: "_Wjjiedbur"
b7p,b,lsb,YX        .. text: "jkefjbloosynokusturuonksqw|rktut{xvpvluqwjsxxvz|rr"
b7p,bgr,lsb,YX      .. text: "kmkgdfghjicdmpnoonszxrnmnnkjuwssuttssuurnknpkjssqrvz}xsmknuxtstx{zxxvqqxwlmptvpnvsklsvxyyywuz"
b1,bgr,msb,YX,prime .. text: "\n(<!-EN@"
b3,abgr,msb,YX,prime.. text: "f_y?guqo}"
b4,r,lsb,YX,prime   .. text: "5T$D32UA60"
b4,b,msb,YX,prime   .. text: "YU.Ib)]3"
b4,bgr,msb,YX,prime .. file: Compiled PSI (v2) data (<$u4\024\240~\264b\266\330/\271Th\272\034\307\3714$\003\234\317C2\2446\350 60\254\361\374\254G\332(\2764$q\262 \261\234\317\376\034O\363Z\244\011"\215\361\014l\266\254\005\322\350\313R\300\313\375r\022\205:h\276\250G\011T\300\363\024\300CR \375\342\013M\372\254\203\262\254\375\022\317\261\\307\375\322\244)
b5p,r,msb,YX,prime  .. text: "\rY9mu\rI%"
b5p,b,msb,YX,prime  .. text: "SK=Se3['"
b6p,g,lsb,YX,prime  .. text: "orpxwuv~"
b6p,g,msb,YX,prime  .. text: ">Q^aFn.a"
b7p,g,msb,YX,prime  .. text: "}#=C\r]]C"
b7p,b,lsb,YX,prime  .. text: "kfdomrjryxmlq}nqqnxrpmiivtorxxwwyvpwvsnlVP|wsvyzyt~|{qyut`Paqyxzz|vuyqvqenenqcrxrvvtouinQxrt}fofrvqpvqu[klwtrjsundefNyak~tqeuyv{tkpooiqtmhrq{hhzxk`qq|mttzvntxx}sry~ytxsduyy`soylzvx~ohgpdioqvm"
b7p,bgr,lsb,YX,prime.. text: "kgfhdpnzmwsukpsxxsxxlnlyq"
b8,bgr,msb,YX,prime .. text: ";O-[wM;O"
b1,bgr,lsb,Xy       .. text: ";\"xjWjWKZn"
b2,b,lsb,Xy         .. text: "`YF1z\n*Y"
b3,r,msb,Xy         .. text: "mMb[TZ2qb"
b3,abgr,msb,Xy      .. file: OpenPGP Secret Key
b3p,b,msb,Xy        .. text: "dA4~SL4\t"
b3p,rgb,lsb,Xy      .. text: "~yPJEK((,,Qz"
b4,r,lsb,Xy         .. text: "GUUeVxu34C"
b4,bgr,msb,Xy       .. file: OpenPGP Secret Key
b5,r,msb,Xy         .. file: OpenPGP Public Key
b5p,rgb,msb,Xy      .. file: OpenPGP Public Key
b6,bgr,msb,Xy       .. file: OpenPGP Secret Key
b6p,g,lsb,Xy        .. text: "w]y|]~rfjor"
b7,r,msb,Xy         .. file: OpenPGP Public Key
b7,rgb,msb,Xy       .. file: OpenPGP Public Key
b7,rgba,msb,Xy      .. file: OpenPGP Public Key
b7p,b,lsb,Xy        .. text: "Usty|x~ynpqiow{rq|uoeuyqsmll}sc|pcqn\\uhchhjqxlacqrikj_c{zvpc\\o{nnz~ynns{rpyotuxvj"
b7p,rgb,msb,Xy      .. file: OpenPGP Public Key
b7p,bgr,lsb,Xy      .. text: "UVs{uuxz|yx}~}yromqqqnhknrwz{zrmqw}|unojdjtzyrpvrjmolmlu|zrfcs}xqecgpwod]eurhdcfhhiijlqvxtlea_ckqsrligjnkd_^cozzzxvtqhc_]anwzwomou{|~}ysoloprwzwrpqxxoovtuuwyyvpjy"
b8,r,msb,Xy         .. text: "OO/ooo//o/"
b8,b,msb,Xy         .. text: "5u]}]]=="
b1,r,lsb,Xy,prime   .. text: "r`3WC2:v"
b1,g,msb,Xy,prime   .. text: "%z-V\t[6#"
b2,b,msb,Xy,prime   .. file: OpenPGP Public Key
b2,rgba,lsb,Xy,prime.. text: "#SO;#K[_"
b3,rgb,lsb,Xy,prime .. text: "'=.x<X\"I"
b4,r,lsb,Xy,prime   .. text: "GUh4%4Fb"
b4,r,msb,Xy,prime   .. text: "`,.\"OBb*"
b4,rgb,lsb,Xy,prime .. text: "=g=-w/^V,R"
b4,bgr,lsb,Xy,prime .. text: "m=7}/'^\\&"
b4,bgr,msb,Xy,prime .. text: "'K>(#[ ~L"
b4,rgba,msb,Xy,prime.. file: QDOS executable '\301\367\274\366\262\361\264\372'
b5p,r,msb,Xy,prime  .. text: "a9=%^Ee5"
b6p,g,lsb,Xy,prime  .. text: "kdfn}zvnpv"
b7,r,msb,Xy,prime   .. file: OpenPGP Secret Key
b7,rgb,msb,Xy,prime .. file: OpenPGP Secret Key
b7,rgba,msb,Xy,prime.. file: OpenPGP Secret Key
b7p,r,msb,Xy,prime  .. file: OpenPGP Secret Key
b7p,b,lsb,Xy,prime  .. text: "su|lkmkvgfehsonlloysmjyl\\xsrhntirrasvvlnsvqnppzwunmojzpzXnu|qrs"
b7p,rgb,msb,Xy,prime.. file: OpenPGP Secret Key
b7p,bgr,lsb,Xy,prime.. text: "s{uz}}mqkzmnjzvmfsgdefitsgn^oxm|lpovyvrolrjiy{ml]|xyswrqhuoqtihosdspanszvuw|l\\oyrrwqqsoqptp`{lwktwnqm{o~jxztqpzyXtndts}mprrhs{~jxkwwm{eoqr^r}aorwyltzj|tutpklmqwqsonpyveplmwpvnpptyqlwvu{pwpw|qunpno{jr\\mkg}rmypuqeoskuzvtiwliitrtlppc"
b7p,abgr,msb,Xy,prime.. file: ddis/ddif
b1,b,msb,yX         .. text: "HFcr:y1<"
b3,r,lsb,yX         .. file: OpenPGP Public Key
b3,g,msb,yX         .. text: ",J{\tKn=i"
b3,abgr,msb,yX      .. file: OpenPGP Secret Key
b3p,r,lsb,yX        .. file: OpenPGP Public Key
b3p,g,lsb,yX        .. text: "V4s&nJq5i<"
b3p,rgb,lsb,yX      .. text: "wM,Pz1\tQvv"
b3p,bgr,lsb,yX      .. text: "`_;;<__9]"
b4,r,lsb,yX         .. text: "Vd34EDEUCDD343"
b4,bgr,msb,yX       .. file: OpenPGP Secret Key
b4,rgba,lsb,yX      .. text: "_\n_,_=o=oO"
b4,abgr,msb,yX      .. text: " ?(?(?$_("
b5,r,lsb,yX         .. text: ")JNQ|)|V3"
b5,r,msb,yX         .. file: OpenPGP Public Key
b5p,rgb,msb,yX      .. file: OpenPGP Public Key
b5p,bgr,lsb,yX      .. file: StuffIt Deluxe Segment (data) : gg\233\330\341\341\342\321\275\253\243\244\266\254\252\254\265\265\317\352\352\340\316\274\264\317\003\362\307\254\234\235\245\232\243\307\320\310\317\306\310\321\330\331\322\277\243\327\373\002\347\233\234\327\330\317\307\277\277\317\331\317\264\305\340\352\342\331\317\305\305\317\321\322\331\341\350\350\340\320\306\316\337\341\341\330\327\316\316\317\327\327\316\327\342\364\374\331\275\317\331\321\331\341\362\363\373\372\340\316\307\310\341\363\005\352\327\331\343\341\341\342\330\315\264\255\311
b6,bgr,msb,yX       .. file: OpenPGP Secret Key
b6p,g,lsb,yX        .. text: "stkpooSar"
b7,r,msb,yX         .. file: OpenPGP Public Key
b7,rgb,msb,yX       .. file: OpenPGP Public Key
b7,rgba,msb,yX      .. file: OpenPGP Public Key
b7p,b,lsb,yX        .. text: "TXgxxohmklszsm"
b7p,rgb,msb,yX      .. file: OpenPGP Public Key
b7p,bgr,lsb,yX      .. text: "UYYYgvyyxuokihljjjmmszzxrnls"
b7p,abgr,msb,yX     .. file: RDI Acoustic Doppler Current Profiler (ADCP)
b1,g,msb,yX,prime   .. file: OpenPGP Public Key
b3,abgr,msb,yX,prime.. text: "r\"oq 7sT"
b3p,b,lsb,yX,prime  .. text: "])i+9%xL/v"
b4,r,lsb,yX,prime   .. text: "5?4cE3cFD"
b4,rgba,lsb,yX,prime.. text: "+_,O,_=oP"
b5,r,msb,yX,prime   .. text: "Zr)%D_K-"
b5,b,msb,yX,prime   .. file: OpenPGP Public Key
b5p,rgb,lsb,yX,prime.. file: RDI Acoustic Doppler Current Profiler (ADCP)
b5p,rgb,msb,yX,prime.. file: MySQL ISAM index file Version -123
b6p,b,msb,yX,prime  .. text: "oO;gOSK;"
b7,bgr,msb,yX,prime .. file: OpenPGP Public Key
b7p,b,lsb,yX,prime  .. text: "Xvjjxjpoozss}t"
b7p,bgr,lsb,yX,prime.. text: "YYvykhjmx|jqpuogoszqszrr|su}~rkpwqtu}snssusomc]mmn{}gqtgux{psp"
b7p,bgr,msb,yX,prime.. file: OpenPGP Public Key
b7p,abgr,lsb,yX,prime.. file: AIX core file 64-bit, \373
b7p,abgr,msb,yX,prime.. file: RDI Acoustic Doppler Current Profiler (ADCP)
b1,g,msb,xY         .. text: "U*w5<<[-]k"
b2,r,msb,xY         .. text: "y)%u%JH9"
b2,rgb,msb,xY       .. file: OpenPGP Secret Key
b2,bgr,msb,xY       .. file: OpenPGP Secret Key
b3,bgr,lsb,xY       .. text: "G}5c=Iz0+"
b3p,g,lsb,xY        .. text: ",f:U:Q@MF"
b3p,rgb,lsb,xY      .. text: "*(wv{{Lm"
b3p,bgr,lsb,xY      .. text: "m)id!m$I"
b4,r,lsb,xY         .. text: "43EweVexR"
b4,r,msb,xY         .. file: PGP encrypted data
b4,rgb,msb,xY       .. text: "C+tj4F+?t"
b4,bgr,msb,xY       .. text: "&Kz4dK6/u"
b6p,r,msb,xY        .. file: OpenPGP Public Key
b6p,g,lsb,xY        .. text: "Zhzxs|v|"
b7,g,lsb,xY         .. file: OpenPGP Secret Key
b7p,b,lsb,xY        .. text: "}obunnmt}{p"
b7p,bgr,lsb,xY      .. text: "|zngblusnqnhmrty}~zvqy"
b1,b,msb,xY,prime   .. text: "k]dZlW(Z"
b1,bgr,lsb,xY,prime .. file: OpenPGP Public Key
b1,abgr,msb,xY,prime.. text: "]3Wq{uQs"
b2,b,lsb,xY,prime   .. text: "N;K9AyV\tb/"
b3,rgba,lsb,xY,prime.. text: "Tx_3ww\\p"
b4,r,lsb,xY,prime   .. text: "B17%sV4SV;"
b4,r,msb,xY,prime   .. text: ",B fLF f"
b5p,r,msb,xY,prime  .. text: "9E!mYM!m"
b6p,abgr,msb,xY,prime.. file: ddis/ddif
b7p,b,lsb,xY,prime  .. text: "}rrxoxWwtsw]pxlpwbuo}d{rynup]pidoxxnt~qii{nty~vr|mqlptktek}twy`jxw~gxqslwjyevlZ{ul^lgssuoxdxphk{ykvxoujrroxme\\ppklv~ipumdmxqwijnqmj}qmjacusz`urhxouqnQ~|ur|j{ptvo~zloqnojgsgir"
b7p,bgr,lsb,xY,prime.. text: "nglshr~v|wrqsxylo"
b7p,abgr,msb,xY,prime.. file: ddis/ddif
b2,r,lsb,Yx         .. text: "L1Jfa@\nLQ"
b2,g,lsb,Yx         .. text: "i@4tNJ\tb"
b2,bgr,msb,Yx       .. text: "WIEqT'y]"
b3,rgba,lsb,Yx      .. text: "73s77q'%"
b3p,r,msb,Yx        .. text: "n+}APbiM"
b3p,b,msb,Yx        .. file: OpenPGP Public Key
b3p,rgb,lsb,Yx      .. text: "[1RWXX\\x"
b4,r,lsb,Yx         .. text: "\"\"4T#C\"4fB34c"
b4,g,msb,Yx         .. text: "7UGDt}p3{"
b4,rgba,lsb,Yx      .. text: ".o,_\n/\n/N"
b4,abgr,msb,Yx      .. text: "/_h_h_/_ "
b5p,g,msb,Yx        .. text: "/KOHh{`'w"
b5p,rgb,msb,Yx      .. text: "i)AAeMUUMi"
b5p,bgr,msb,Yx      .. text: "m5II}K[G[}"
b5p,abgr,msb,Yx     .. file: RDI Acoustic Doppler Current Profiler (ADCP)
b6p,g,lsb,Yx        .. text: "}sxrwl|{"
b6p,rgb,msb,Yx      .. text: "CCK[kk[S"
b6p,bgr,msb,Yx      .. text: "[+SS{WwOw{"
b6p,abgr,msb,Yx     .. file: RDI Acoustic Doppler Current Profiler (ADCP)
b7,g,lsb,Yx         .. file: OpenPGP Secret Key
b7p,b,lsb,Yx        .. text: "|{smdnvwiwjnpqtnupsvyruxegx}{yvsuow}}qie_Vfhyvxvqqt{trm}wttrqx|rllgxonpiamfmorquprryopuhupslpyirtoqwvpswsz|slhq{wkrklqmupystw{wuuiit{zxttrmt|}smj^^h_wvtvsqvxsnl{vypsox}pmoe}tjpq`fioouu{uoszklphokrprwq{rmowrqwwpnwqsuswrnkoomgurxxx{{ywlqttv{ttvsiluxsvvnrr]nq"
b7p,bgr,lsb,Yx      .. text: "||{vsoljddntvxvnirvnjloppqpstuoquspprrw}xrsuuvxpecfnx}|{zzyvvussurnrvz}~|wqjigdb^ZV]fdiqx{wqy"
b7p,abgr,msb,Yx     .. file: RDI Acoustic Doppler Current Profiler (ADCP)
b8,r,lsb,Yx         .. file: PC formatted floppy with no filesystem
b8,g,msb,Yx         .. text: "{;[[{GGGG{"
b2,r,lsb,Yx,prime   .. text: "TB=q425K"
b2,rgb,lsb,Yx,prime .. file: OpenPGP Secret Key
b2,rgba,lsb,Yx,prime.. file: OpenPGP Secret Key
b3,r,lsb,Yx,prime   .. text: "I,:y;2H\""
b3,r,msb,Yx,prime   .. file: OpenPGP Public Key
b3,rgb,lsb,Yx,prime .. file: OpenPGP Public Key
b3,rgba,lsb,Yx,prime.. file: OpenPGP Public Key
b3p,b,msb,Yx,prime  .. text: "kCn.\n+0a"
b3p,rgb,lsb,Yx,prime.. file: OpenPGP Secret Key
b4,r,lsb,Yx,prime   .. text: "f\"e2$4#7EV@"
b4,b,msb,Yx,prime   .. text: ">U~K9%if"
b4,rgba,lsb,Yx,prime.. text: ",oNo<o<_"
b5p,b,msb,Yx,prime  .. text: "=K}W3+sm"
b5p,bgr,msb,Yx,prime.. file: OpenPGP Secret Key
b6p,g,lsb,Yx,prime  .. text: "xdxcxt~vxx"
b6p,rgb,msb,Yx,prime.. file: OpenPGP Public Key
b7p,b,lsb,Yx,prime  .. text: "{otspqrpvsw]rvwlnevwqts}nquntnzrtrlk{jowpsov{lkpursyslptvoprvlytmwprtnrupkrrrhufvtktqxyooeprzfuqpuuwxdoiqqtlglrvwplqdm^r}vkb^t{tpwluhqszxmqwqvxltmuf}khoxpszrs|qdmbmlrhmmys}uXqqqrxtqj}stoptsxtwtksp_w}xqlPkwnwytl_wrmupxswyjvo"
b7p,b,msb,Yx,prime  .. text: "v.v^N.N6"
b7p,bgr,lsb,Yx,prime.. text: "{vojtxrnpuqrrup}vur~wb]{rywhvslhopdowqwkqstpsv}zolpvuwoxttn}{esyuhsllljkzokhnrwwptrworvxzvmqjwpttvsusgxws~mpqtupwtospqsyvumtyvtmmrwnqurlt|ourxtvqmkvsqr}slhytgfywdtpjjtuqsxqx{nonvdnpxsqzlgluvqcqttnu_wsyueqoshfqzpwttlqgsldruv`vspxm|psdqlk^dsx|wvpk"
b8,bgr,msb,Yx,prime .. text: "/m;Om{/m;"
```