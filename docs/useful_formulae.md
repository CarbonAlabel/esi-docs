# Warp-in Points

A warp-in point is where your ship will land in space when warping to an object.

Many external factors may disrupt a warp, e.g. warp disruption fields, insufficient electrical capacity, warp jitter, etc.; these formulas do not account for these phenomenas, they assume perfect conditions.

## Ordinary Objects

An ordinary object is any object that does not fall withing any of the other categories described below.

Let the 3D vectors <img src="/docs/tex/5a9c317bfbcdf70858bfb589ac657ffb.svg?invert_in_darkmode&sanitize=true" align=middle width=15.113645249999989pt height=14.15524440000002pt/> and <img src="/docs/tex/ab5e4577f8a696e1e41679990c7a8c3b.svg?invert_in_darkmode&sanitize=true" align=middle width=14.47493684999999pt height=14.15524440000002pt/> represent the object's position and the warp's origin, respectively; and <img src="/docs/tex/120f2b8ffd83f3e86111a829382f2763.svg?invert_in_darkmode&sanitize=true" align=middle width=10.747741949999996pt height=23.488575000000026pt/> the directional vector from <img src="/docs/tex/ab5e4577f8a696e1e41679990c7a8c3b.svg?invert_in_darkmode&sanitize=true" align=middle width=14.47493684999999pt height=14.15524440000002pt/> to <img src="/docs/tex/5a9c317bfbcdf70858bfb589ac657ffb.svg?invert_in_darkmode&sanitize=true" align=middle width=15.113645249999989pt height=14.15524440000002pt/>. Let <img src="/docs/tex/2b319ec920b08f6cb69ea5b438059514.svg?invert_in_darkmode&sanitize=true" align=middle width=7.87295519999999pt height=14.15524440000002pt/> be the object's radius.

The object's warp-in point is the vector <img src="/docs/tex/0d33cf8348cd44f2a4981505b75408b1.svg?invert_in_darkmode&sanitize=true" align=middle width=80.75516459999999pt height=23.488575000000026pt/>.

## Large Objects

A large object is any celestial body whose radius exceeds 90 kilometres (180 kilometres in diameter), except planets.

Let <img src="/docs/tex/e4fd027188c5ecbf6abde58e5b94bcd5.svg?invert_in_darkmode&sanitize=true" align=middle width=9.39498779999999pt height=14.15524440000002pt/>, <img src="/docs/tex/a3bd584dc0ef15b1884333c4d22133cf.svg?invert_in_darkmode&sanitize=true" align=middle width=8.649225749999989pt height=14.15524440000002pt/>, and <img src="/docs/tex/0b8b503aecef5e3fa3496a107142474e.svg?invert_in_darkmode&sanitize=true" align=middle width=8.367621899999993pt height=14.15524440000002pt/> represent the object's coordinates. Let <img src="/docs/tex/2b319ec920b08f6cb69ea5b438059514.svg?invert_in_darkmode&sanitize=true" align=middle width=7.87295519999999pt height=14.15524440000002pt/> be the object's radius.

The object's warp-in point is the vector <img src="/docs/tex/0c8dd98c5c648162704e390247de6cf9.svg?invert_in_darkmode&sanitize=true" align=middle width=468.6982542pt height=24.65753399999998pt/>

## Planets

The warp-in point of a planet is determined by the planet's ID, its location, and radius.

Let <img src="/docs/tex/e4fd027188c5ecbf6abde58e5b94bcd5.svg?invert_in_darkmode&sanitize=true" align=middle width=9.39498779999999pt height=14.15524440000002pt/>, <img src="/docs/tex/a3bd584dc0ef15b1884333c4d22133cf.svg?invert_in_darkmode&sanitize=true" align=middle width=8.649225749999989pt height=14.15524440000002pt/>, and <img src="/docs/tex/0b8b503aecef5e3fa3496a107142474e.svg?invert_in_darkmode&sanitize=true" align=middle width=8.367621899999993pt height=14.15524440000002pt/> represent the planet's coordinates. Let <img src="/docs/tex/2b319ec920b08f6cb69ea5b438059514.svg?invert_in_darkmode&sanitize=true" align=middle width=7.87295519999999pt height=14.15524440000002pt/> be the planet's radius.

The planet's warp-in point is the vector <img src="/docs/tex/b5d2994c951b0023679b739efc932cbc.svg?invert_in_darkmode&sanitize=true" align=middle width=253.80505754999993pt height=27.94539330000001pt/>
where:

<p align="center"><img src="/docs/tex/d70b9a2bb64fce1cbe2cd8e35cd60b5f.svg?invert_in_darkmode&sanitize=true" align=middle width=164.77351935pt height=16.438356pt/></p>
<p align="center"><img src="/docs/tex/9ccfdfa5975cf98b33b8ed54fc6457fc.svg?invert_in_darkmode&sanitize=true" align=middle width=227.25574409999996pt height=39.452455349999994pt/></p>
<p align="center"><img src="/docs/tex/879009560e091a3d0673a3f225a8c47f.svg?invert_in_darkmode&sanitize=true" align=middle width=373.68164625pt height=42.80407395pt/></p>


Now, <img src="/docs/tex/e62c4c55196ed02fd2fa7c51b8c03611.svg?invert_in_darkmode&sanitize=true" align=middle width=7.710416999999989pt height=21.68300969999999pt/> is a special snowflake. Its value is the Python equivalent of `(random.Random(planetID).random() - 1.0) / 3.0`.

### Example Implementation

```python
import math
import random

def warpin(id, x, y, z, r):
    j = (random.Random(id).random() - 1.0) / 3.0
    t = math.asin(x/abs(x) * (z/math.sqrt(x**2 + z**2))) + j
    s = 20.0 * (1.0/40.0 * (10 * math.log10(r/10**6) - 39))**20.0 + 1.0/2.0
    s = max(0.5, min(s, 10.5))
    d = r*(s + 1) + 1000000

    return (x + d * math.sin(t), y + 1.0/2.0 * r * math.sin(j), z - d * math.cos(t))
```

# Skillpoints

## Skillpoints needed per level

The skillpoints needed for a level depend on the skill rank.

<p align="center"><img src="/docs/tex/fc84a6590620b4522f72a10968385fc3.svg?invert_in_darkmode&sanitize=true" align=middle width=316.78308254999996pt height=20.1205785pt/></p>
 

### Skillpoints for common ranks

<table>
<thead>
<tr><th>Rank</th><th>Level 1</th><th>Level 2</th><th>Level 3</th><th>Level 4</th><th>Level 5</th></tr>
</thead>
<tbody>
<tr><th>1</th> <td>250</td>  <td>1.414</td> <td>8.000</td>  <td>45.254</td> <td>256.000</td></tr>
<tr><th>2</th> <td>500</td>  <td>2.828</td> <td>16.000</td> <td>90.509</td> <td>512.000</td></tr>
<tr><th>3</th> <td>750</td>  <td>4.242</td> <td>24.000</td> <td>135.764</td><td>768.000</td></tr>
<tr><th>4</th> <td>1.000</td><td>5.656</td> <td>32.000</td> <td>181.019</td><td>1.024.000</td></tr>
<tr><th>5</th> <td>1.250</td><td>7.071</td> <td>40.000</td> <td>226.274</td><td>1.280.000</td></tr>
<tr><th>6</th> <td>1.500</td><td>8.485</td> <td>48.000</td> <td>271.529</td><td>1.536.000</td></tr>
<tr><th>7</th> <td>1.750</td><td>9.899</td> <td>56.000</td> <td>316.783</td><td>1.792.000</td></tr>
<tr><th>8</th> <td>2.000</td><td>11.313</td><td>64.000</td> <td>362.038</td><td>2.048.000</td></tr>
<tr><th>9</th> <td>2.250</td><td>12.727</td><td>72.000</td> <td>407.293</td><td>2.304.000</td></tr>
<tr><th>10</th><td>2.500</td><td>14.142</td><td>80.000</td> <td>452.548</td><td>2.560.000</td></tr>
<tr><th>11</th><td>2.750</td><td>15.556</td><td>88.000</td> <td>497.803</td><td>2.816.000</td></tr>
<tr><th>12</th><td>3.000</td><td>16.970</td><td>96.000</td> <td>543.058</td><td>3.072.000</td></tr>
<tr><th>13</th><td>3.250</td><td>18.384</td><td>104.000</td><td>588.312</td><td>3.328.000</td></tr>
<tr><th>14</th><td>3.500</td><td>19.798</td><td>112.000</td><td>633.567</td><td>3.584.000</td></tr>
<tr><th>15</th><td>3.750</td><td>21.213</td><td>120.000</td><td>678.822</td><td>3.840.000</td></tr>
<tr><th>16</th><td>4.000</td><td>22.627</td><td>128.000</td><td>724.077</td><td>4.096.000</td></tr>
</tbody>
</table>

## Skillpoints per minute

The skillpoints generated each minute depend on the primary <img src="/docs/tex/90e928b5d905ee7bd1e2e9fbdea263d9.svg?invert_in_darkmode&sanitize=true" align=middle width=72.51345584999999pt height=24.65753399999998pt/> and secondary attribute <img src="/docs/tex/2818a16e48dfdac21c7e2a2fef85720f.svg?invert_in_darkmode&sanitize=true" align=middle width=82.73746304999999pt height=24.65753399999998pt/> of the skill.

<p align="center"><img src="/docs/tex/c09c84c75743a75dce81c94a7b5d6600.svg?invert_in_darkmode&sanitize=true" align=middle width=314.67782609999995pt height=29.47417935pt/></p>


# Combat

## Target lock time

The target lock time (<img src="/docs/tex/1715cd52b399fd871aab7a7cf4e81424.svg?invert_in_darkmode&sanitize=true" align=middle width=66.37144634999999pt height=20.221802699999984pt/>) in seconds depends on the ship's scan resolution (<img src="/docs/tex/e8de4c1b2051364afda13ddbc4852439.svg?invert_in_darkmode&sanitize=true" align=middle width=7.7054801999999905pt height=14.15524440000002pt/>) and the target's signature radius (<img src="/docs/tex/2b319ec920b08f6cb69ea5b438059514.svg?invert_in_darkmode&sanitize=true" align=middle width=7.87295519999999pt height=14.15524440000002pt/>)

<p align="center"><img src="/docs/tex/7e21e67710b4fe7a34b6b824350575ac.svg?invert_in_darkmode&sanitize=true" align=middle width=180.0895206pt height=37.099754999999995pt/></p>


## Alignment time

The ship alignment time (<img src="/docs/tex/e4fc863f0f793c02543fc36f1971f027.svg?invert_in_darkmode&sanitize=true" align=middle width=36.89315684999998pt height=20.221802699999984pt/>) depends on the ship's inertia modifier (<img src="/docs/tex/8fceb32bd3f6803b77bbe1b1758a60b6.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>) and the ships mass (<img src="/docs/tex/7371e4a1b4ff766095a123b7f0023f5c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.433101099999991pt height=14.15524440000002pt/>)

<p align="center"><img src="/docs/tex/6112fc0fdb8d7c91ec5746389e803a4b.svg?invert_in_darkmode&sanitize=true" align=middle width=141.54538695pt height=34.7253258pt/></p>
