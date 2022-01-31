# assignment2-aluri
# Harikiran Aluri
#### gismath

The sea is one of the most beautiful blessings for man, **which shows the greatness of the Creator.**  Words can’t describe the sea beauty and charm, which is an inspiration to many poets and writers. Poems and thoughts that talked about sea are uncountable.

The beach is my favorite place. **Sit down to relax and think.** I also go to it to practice many activities and games.

I join my friends in playing treasure hunt in the sand, which is based on hiding various objects down the sand and writing instructions on paper cards to help others reach them. 

--------------------------------------------------------------

# Gannavaram Airport
## Gannavaram Airport is the closest Airport to my Food location

   - After getting out from the restarunt go straight towards gorantlaa

   - than take left so that you can enter into highway

   - go straight for 2km so that u can get a bypass

   - after entering into the bypass take a immidate left and than immidate right

## Food items

1. Chicken Mandi
2. Mutton Mandi
3. Prawns Mandi


sMore about me (https://github.com/harichowdary-aluri/assignment2-aluri/blob/main/AboutMe.md).

------------------------------------------------------------------------

# Sports

| Name   | Location   | Amount   |
|--------|------------|----------|
| Volley Ball   |Guntur   | $40   |
| Basket Ball   | Vijayawada   | $20   |
| Throw Ball   | Hyderabad   |$15   |

-------------------------------------------------------------------------

# Quotes

>The best thing about gaining knowledge is nobody can take it from you. *Venkatest*

>Knowledge is divine. *Brahma*

--------------------------------------------------------------------------

# Geometry Convex hull

>In geometry, the convex hull or convex envelope or convex closure of a shape is the smallest convex set that contains it. The convex hull may be defined either as the intersection of all convex sets containing a given subset of a Euclidean space, or equivalently as the set of all convex combinations of points in the subset. For a bounded subset of the plane, the convex hull may be visualized as the shape enclosed by a rubber band stretched around the subset.

Know more (https://en.wikipedia.org/wiki/Convex_hull)

struct pt {
    double x, y;
};

int orientation(pt a, pt b, pt c) {
    double v = a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y);
    if (v < 0) return -1; // clockwise
    if (v > 0) return +1; // counter-clockwise
    return 0;
}

bool cw(pt a, pt b, pt c, bool include_collinear) {
    int o = orientation(a, b, c);
    return o < 0 || (include_collinear && o == 0);
}
bool collinear(pt a, pt b, pt c) { return orientation(a, b, c) == 0; }

void convex_hull(vector<pt>& a, bool include_collinear = false) {
    pt p0 = *min_element(a.begin(), a.end(), [](pt a, pt b) {
        return make_pair(a.y, a.x) < make_pair(b.y, b.x);
    });
    sort(a.begin(), a.end(), [&p0](const pt& a, const pt& b) {
        int o = orientation(p0, a, b);
        if (o == 0)
            return (p0.x-a.x)*(p0.x-a.x) + (p0.y-a.y)*(p0.y-a.y)
                < (p0.x-b.x)*(p0.x-b.x) + (p0.y-b.y)*(p0.y-b.y);
        return o < 0;
    });
    if (include_collinear) {
        int i = (int)a.size()-1;
        while (i >= 0 && collinear(p0, a[i], a.back())) i--;
        reverse(a.begin()+i+1, a.end());
    }

    vector<pt> st;
    for (int i = 0; i < (int)a.size(); i++) {
        while (st.size() > 1 && !cw(st[st.size()-2], st.back(), a[i], include_collinear))
            st.pop_back();
        st.push_back(a[i]);
    }

    a = st;
}

Much more to know (https://cp-algorithms.com/geometry/convex-hull.html)

