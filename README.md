# PageRank
**페이지랭크**

An interactive web demo on PageRank, from eigenvector centrality to the random surfer behind Google. It is demo 10 in the [interactive demos](https://lshlj82.github.io/netsci-course-GNU/) for *Network Science* (네트워크 과학) in the Department of Physics, Gyeongsang National University.

Created by **Claude Opus 5.5**, based on the lecture slides by **Prof. Sang Hoon Lee**.
이상훈 교수의 강의 슬라이드를 바탕으로 Claude Opus 5.5가 만들었습니다.

**Live page:** https://lshlj82.github.io/PageRank/ (English) · https://lshlj82.github.io/PageRank/ko.html (한국어)

## Files

| File | Description |
| --- | --- |
| `index.html` | English page |
| `ko.html` | Korean page (한국어) |
| `README.md` | This file |

The two pages share identical code and differ only in the language they display. Each one is a single self-contained HTML file with no build step and no libraries. The only external request is to Google Fonts (IBM Plex Sans and Fraunces for Latin text, and Noto Serif KR for Korean, as on the course page). If that request fails, the pages fall back to system fonts.

## What's inside

1. **Importance from important neighbors.** Eigenvector centrality, x<sub>i</sub> ∝ Σ<sub>j</sub> a<sub>ij</sub> x<sub>j</sub>, which becomes the eigenvector equation **Ax** = λ**x**. It is solved step by step by repeating x ← **A**x on a 12-node network. In that network the node with the most links (a hub of leaves) ends up far less central than the nodes of a tightly knit group. A box explains why directed links need more than this, and the section ends with Marissa Mayer's line about eigenvectors.
2. **The random surfer.** On a ten-page Web, the surfer follows a random link with probability 1 − α and jumps to a random page with probability α. The surfer always jumps from the page with no outgoing links. The fraction of visits slowly approaches the PageRank of Eq. (4.1) in Menczer, Fortunato and Davis.
3. **The power method.** R<sub>0</sub> = 1/N, then the update applied to all pages at once. Clicking a page shows its update written out with numbers, as in Box 4.2 (R(3) = 0.2/5 + 0.3/2). The page also shows Σ R = 1 and a log-scale convergence plot with the (1 − α)<sup>t</sup> bound. Pages without outgoing links are spread over all pages.
4. **Why not just count incoming links?** Pages 0 and 7 both have five incoming links but very different PageRanks, and page 6 reaches second place with a single link from page 0. A link-farm slider adds fake pages that link to page 1 and back. Six fake pages are enough to put page 1 at the top.
5. **PageRank on a large Web-like network.** A 3000-page network grown by directed preferential attachment (Price's model). The page plots the cumulative PageRank distribution on log–log axes next to that of k<sub>in</sub>/L, and a scatter plot of PageRank against in-degree.
6. **In code.** `nx.pagerank(D)`, with a note that NetworkX's `alpha` is the damping factor (0.85), that is, 1 − α in the textbook's notation.

## Notes on the model

- PageRank is computed with the power method to a tolerance of 10<sup>−13</sup> (10<sup>−12</sup> for the large network). The PageRank of pages without outgoing links is spread uniformly over all pages, which is also NetworkX's default.
- On the ten-page Web, `nx.pagerank(D, alpha=0.85)` gives the same values as the demo at α = 0.15 (page 0: 0.265, page 6: 0.251, page 7: 0.105).
- The large network is synthetic. It reproduces the qualitative shape of the Web host graph's distribution, not its values.
- The pages support light and dark mode (the choice is shared with the other course demos) and adapt to phone screens.

## Running it

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/
```

To publish with GitHub Pages, go to **Settings → Pages**, choose **Deploy from a branch**, and select `main` and the root folder.

## References

- S. Brin and L. Page, "The anatomy of a large-scale hypertextual Web search engine," *Computer Networks and ISDN Systems* **30**, 107 (1998).
- F. Menczer, S. Fortunato, and C. A. Davis, *A First Course in Network Science* (Cambridge University Press, 2020), Box 4.2. 한국어판 『네트워크 분석』 (에이콘출판사, 2022).
- D. J. de S. Price, "A general theory of bibliometric and other cumulative advantage processes," *J. Am. Soc. Inf. Sci.* **27**, 292 (1976).
- Prof. Sang Hoon Lee, lecture slides for Network Science (이상훈 교수, 네트워크 과학 강의 슬라이드).
