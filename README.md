# TopTherm Forecast File Format

This is a reverse-engineered description of the forecast file format used by the [DWD TopTherm](http://www.dwd.de/bvbw/appmanager/bvbw/dwdwwwDesktop?_nfpb=true&portletMasterPortlet_i1gsbDocumentPath=Content%2FLuftfahrt%2FInternetservice%2Fjtt.html) application.


## Download URL

The forecast files can be downloaded as bzip2 archives from the following URL:

https://www.flugwetter.de/scripts/getfile.php?src=jtt/15082106p12.gra.bz2

- `150821` - this forecast is for the `2015-08-21` date
- `06` - ???
- `p12` - ???


### Examples

    Yesterday:            jtt/15081806.gra.bz2
    Today:                jtt/15081906.gra.bz2
    Tomorrow:             jtt/15082006p12.gra.bz2
    Day after tomorrow:   jtt/15082106p12.gra.bz2

These URLs were downloaded by the original Java application at `2015-08-19T17:55:00Z`.


## Format Example

This shows the forecast of the region "Engadin". The file inside the bzip2 archive contains all regions, each divided
by two blank lines.

```
ZCZC
gggg105
GG105 Engadin
, Fr 23.05.2015 [EU 00z +24h, LW, ET  30%@2300m]

UTC     T  Td Vario [0.5m/s]       Thermik Cumuli Basis-Top CL CM CH   Wind   T  NS  tPFD  kum |  Hang  Alt   Wind   dPFD  kum
hh:mm [C] [C]    2km  3km  4km  5km [m/s] [octas] [m] - [m]  [octas] [deg/kt]        [km] [km] | [m/s]  [m] [deg/kt] [km] [km]
06:00   7   5 -|-:----:----:----:--           ||| 1500-1700  3  0  0   11  6                   |  0.18 3000    8  5
06:30   8   6 -.-:....:----:----:--                          0  0  0   23  5                   |  0.18 3000   15  5
07:00   9   6 .....111.----:----:--  0.3               2900  0  0  0   23  5                   |  0.18 3000   15  5
07:30  10   6 1111112111.--:----:--  0.6               3200  0  0  0    9  6                   |  0.18 3000    9  5
08:00  11   6 11111122211--:----:--  0.8               3300  0  0  0    6  6                   |  0.18 3000    9  5
08:30  12   6 1111.12222.--:----:--  0.9               3400  0  0  0  351  6                   |  0.18 3000  354  5
09:00  13   6 11111222321--:----:--  1.0               3300  0  0  0  353  6           29   29 |  0.18 3000  354  5
09:30  14   6 12121223332--:----:--  1.1               3500  0  0  0  357  6           30   60 |  0.18 3000  358  5
10:00  16   6 11122233443.-:----:--  1.4               3500  0  0  0  357  6           35   95 |  0.18 3000  358  5
10:30  17   5 122222334443------:--  1.7        * 3700-3700  1  2  0  354  6           38  133 |  0.18 3000  350  5
11:00  18   5 12222334444*2-----:--  1.7        * 3500-3600  1  2  0  352  6           37  170 |  0.18 3000  350  5
11:30  19   4 12222333344***----:--  1.7        * 3600-4000  1  4  0  339  7           38  208 |  0.18 3000  351  5
12:00  20   4 12223334445***----:--  1.9       ** 3500-4100  1  4  0  340  7           39  247 |  0.18 3000  351  5
12:30  20   3 122233333333***---:--  1.6       ** 3700-4200  1  5  0  333  8           36  283 |  0.18 3000  352  5
13:00  21   3 122333334443***---:--  1.7       ** 3700-4300  1  5  0  333  8           38  321 |  0.18 3000  352  5
13:30  21   3 122233333343*****-:--  1.6       ** 3700-4600  1  3  0  334  9           36  357 |  0.21 3000  355  6
14:00  21   2 122233334443*****-:--  1.7       ** 3700-4600  1  3  0  334  9           37  395 |  0.21 3000  355  6
14:30  22   2 122333344443*****-:--  1.8       ** 3700-4700  1  3  0  339  8           39  434 |  0.24 3000    4  7
15:00  22   2 122333344444*****-:--  1.9       ** 3700-4700  1  3  0  339  8           40  473 |  0.24 3000    4  7
15:30  22   2 122333334443*****-:--  1.8       ** 3700-4700  1  1  0  340  8           39  512 |  0.24 3000    1  7
16:00  22   2 .11223333333******:--  1.5       ** 3700-4800  1  1  0  340  8           36  548 |  0.24 3000    1  7
16:30  22   2 .11222222332*****-:--  1.3       ** 3700-4600  1  1  0  335  7           33  580 |  0.21 3000  359  6
17:00  22   2 .111..111...****--:--  0.3       ** 3800-4500  1  1  0  330  8                   |  0.21 3000  359  6
17:30  21   3 ---:..--:---***---:--            ** 3800-4300  0  7  1  332  7                   |  0.00 3300  332  7
18:00  21   3 ---:....:----:----:--                          0  0  1    9  8                   |  0.21 3000  351  6
NNNN
```

## Format Description

### Framing

```
ZCZC
...
NNNN
```

Each region seems to be framed by two lines reading `ZCZC` and `NNNN`. 

### Region Code and Name

```
gggg105
GG105 Engadin
```

The first two lines of the content describe the region code and name. In Germany the region code is identical to the
[GAFOR](https://de.wikipedia.org/wiki/GAFOR) code.


### Forecast Date

```
, Fr 23.05.2015 [EU 00z +24h, LW, ET  30%@2300m]
```

The third line always seems to start with `, ` followed by the date that this forecast is for and some more
unidentified information.
