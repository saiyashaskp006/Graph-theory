%====================================================================
% Graph Theory Explained  --  compile with pdflatex (twice)
%====================================================================
\documentclass[12pt,a4paper]{article}
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage[margin=1in]{geometry}
\usepackage{amsmath,amssymb}
\usepackage{xcolor}
\usepackage{enumitem}
\usepackage{tikz}
\usetikzlibrary{arrows.meta,positioning,calc}
\usepackage{titlesec}
\usepackage{hyperref}
\hypersetup{colorlinks=true,linkcolor=blue,urlcolor=blue,pdftitle={Graph Theory for Kids}}

\titleformat{\section}{\Large\bfseries\color{blue!60!black}}{\thesection}{0.6em}{}
\titleformat{\subsection}{\large\bfseries}{\thesubsection}{0.6em}{}

%--------------------- Boxes ----------------------------------------
\newcommand{\kidbox}[1]{\par\medskip\noindent
  \fcolorbox{green!50!black}{green!8}{\parbox{\dimexpr\linewidth-2\fboxsep-2\fboxrule}{%
  \textbf{\color{green!40!black}In kid words:} #1}}\par\medskip}
\newcommand{\defbox}[1]{\par\medskip\noindent
  \fcolorbox{blue!60!black}{blue!6}{\parbox{\dimexpr\linewidth-2\fboxsep-2\fboxrule}{%
  \textbf{\color{blue!60!black}Proper definition:} #1}}\par\medskip}
\newcommand{\realbox}[1]{\par\medskip\noindent
  \fcolorbox{orange!70!black}{orange!8}{\parbox{\dimexpr\linewidth-2\fboxsep-2\fboxrule}{%
  \textbf{\color{orange!60!black}Real life:} #1}}\par\medskip}
\newcommand{\tryit}[1]{\par\medskip\noindent
  \fcolorbox{purple!60}{purple!6}{\parbox{\dimexpr\linewidth-2\fboxsep-2\fboxrule}{%
  \textbf{\color{purple!70!black}Try it!} #1}}\par\medskip}

%--------------------- TikZ styles ----------------------------------
\tikzset{
  v/.style={circle,draw,fill=yellow!40,minimum size=6mm,inner sep=0pt,font=\scriptsize},
  v2/.style={v,fill=pink!70},
  hl/.style={very thick,red!70!black},
  every picture/.style={>={Stealth[length=2mm]}}
}
% picture beside text: \pic{left text}{tikz picture}
\newcommand{\sidebyside}[2]{\noindent
  \begin{minipage}[c]{0.56\linewidth}#1\end{minipage}\hfill
  \begin{minipage}[c]{0.40\linewidth}\centering#2\end{minipage}\par\medskip}

\title{\Huge Graphs Theory\\[4pt]\large Graph Theory Explained in minutes --- With Proper Definitions}
\author{Sai Yashas KP}
\date{}

\begin{document}
\maketitle
\tableofcontents
\bigskip

%====================================================================
\section{What Is a Graph?}
%====================================================================
\kidbox{Draw some \textbf{dots}. Join some of the dots with \textbf{lines}. That's it ---
you've drawn a \emph{graph}! (Not the bar-chart kind of graph. This one is a map of
\emph{who is connected to whom}.)}

\sidebyside{%
Think of a class of 4 friends: Asha, Ben, Chitra and Dev. Each friend is a dot. If two
people are friends, we draw a line between them.}{%
\begin{tikzpicture}
  \node[v] (a) at (0,0){A}; \node[v] (b) at (2,0){B};
  \node[v] (c) at (0,1.6){C}; \node[v] (d) at (2,1.6){D};
  \draw (a)--(b)--(d)--(c)--(a); \draw (b)--(c);
\end{tikzpicture}}

\defbox{A \textbf{graph} $G=(V,E)$ consists of a set $V$ of \textbf{vertices} (the dots)
and a set $E$ of \textbf{edges} (the lines), where each edge joins two vertices.
In the picture above, $V=\{A,B,C,D\}$ and $E=\{AB,BD,DC,CA,BC\}$.}

\subsection{Words you must know}
\begin{center}
\begin{tabular}{@{}p{3cm}p{5.2cm}p{5.8cm}@{}}
\hline
\textbf{Word} & \textbf{Kid meaning} & \textbf{Proper definition}\\ \hline
Vertex (node) & A dot. & An element of $V$.\\[2pt]
Edge (link) & A line between two dots. & A pair of vertices $\{u,v\}\in E$.\\[2pt]
Degree & How many lines touch a dot (how many friends you have). & $\deg(v)$ = number of edges at $v$.\\[2pt]
Neighbour & A dot you're directly joined to. & $u$ is adjacent to $v$ if $\{u,v\}\in E$.\\[2pt]
Path & Walking along lines without visiting a dot twice. & A sequence of distinct vertices, each adjacent to the next.\\[2pt]
Cycle & A path that comes back to where it started. & A path whose last vertex is adjacent to the first.\\[2pt]
Loop & A line that starts and ends at the \emph{same} dot. & An edge $\{v,v\}$.\\ \hline
\end{tabular}
\end{center}

\tryit{In the friends graph above, what is the degree of B? (Count the lines touching B.)
\emph{Answer: 3 --- B is friends with A, D and C.}}

\textbf{Handshake rule.} If every person shakes hands with their friends, the total number
of hand-ends is double the number of handshakes. Formally,
\[\sum_{v\in V}\deg(v)=2\,|E|.\]
So the sum of all degrees is \emph{always even}. (Check: $2+3+3+2=10=2\cdot5$.)

%====================================================================
\section{Kinds of Graphs}
%====================================================================

\subsection{Undirected graph: friendships}
\kidbox{If I'm your friend, you're my friend. The line works both ways, so it has no arrow.}
\defbox{In an \textbf{undirected graph} an edge $\{u,v\}$ is the same as $\{v,u\}$.}
\realbox{Facebook friendships, roads that allow two-way traffic.}

\subsection{Directed graph (digraph): following}
\kidbox{On Instagram, you can follow a celebrity without them following you back.
We draw an \textbf{arrow} to show the direction.}
\sidebyside{\defbox{In a \textbf{directed graph} each edge (called an \emph{arc}) is an ordered pair
$(u\to v)$, and $(u\to v)\neq(v\to u)$. Each vertex has an \emph{in-degree} (arrows coming in) and an
\emph{out-degree} (arrows going out).}}{%
\begin{tikzpicture}
  \node[v] (a) at (0,0){Me}; \node[v] (b) at (2,0){You}; \node[v] (c) at (1,1.6){Star};
  \draw[->] (a)--(b); \draw[->] (b)--(c); \draw[->] (a)--(c);
  \draw[->] (c) to[bend left=18] (b);
\end{tikzpicture}}
\realbox{Twitter/Instagram follows, one-way streets, web links, ``Task A must finish before Task B''.}

\subsection{Weighted graph: roads with distances}
\kidbox{Some lines are longer or harder than others. We write a \textbf{number} on the line
to say how much it costs: kilometres, minutes or rupees.}
\sidebyside{\defbox{A \textbf{weighted graph} $G=(V,E,w)$ has a function $w:E\to\mathbb{R}$ giving every
edge a number (its weight).}}{%
\begin{tikzpicture}
  \node[v] (h) at (0,0){Home}; \node[v] (s) at (2.2,1.3){Shop}; \node[v] (p) at (2.2,-1.3){Park};
  \node[v] (sc) at (4.4,0){School};
  \draw (h)--(s) node[midway,above left]{\scriptsize 4 km};
  \draw (h)--(p) node[midway,below left]{\scriptsize 2 km};
  \draw (s)--(sc) node[midway,above right]{\scriptsize 3 km};
  \draw (p)--(sc) node[midway,below right]{\scriptsize 6 km};
  \draw (s)--(p) node[midway,right]{\scriptsize 1 km};
\end{tikzpicture}}
\tryit{Shortest way from Home to School? Home$\to$Park$\to$Shop$\to$School $=2+1+3=6$ km. Home$\to$Shop$\to$School $=7$ km.
So the 6 km route wins! Google Maps does exactly this kind of search (the idea is called \emph{Dijkstra's algorithm}).}

\subsection{Simple graph, multigraph and pseudograph}
\kidbox{Imagine two cities joined by \emph{two} separate bridges. That is allowed in some graphs.
And a road that leaves a town and loops back to the same town? Also allowed in some graphs.}
\sidebyside{\defbox{A \textbf{simple graph} has \emph{no loops} and \emph{no parallel edges}.
A \textbf{multigraph} allows parallel (multiple) edges. A \textbf{pseudograph} allows both loops and parallel edges.}}{%
\begin{tikzpicture}
  \node[v] (a) at (0,0){1}; \node[v] (b) at (2,0){2}; \node[v] (c) at (1,1.5){3};
  \draw (a) to[bend left=20] (b); \draw (a) to[bend right=20] (b);
  \draw (b)--(c); \draw (c)--(a); \draw (c) to[loop above,min distance=7mm] (c);
\end{tikzpicture}}

\subsection{Connected and disconnected graphs}
\kidbox{If you can walk from \emph{any} dot to \emph{any} other dot, the graph is connected.
If some dots are stranded on an island, it is disconnected.}
\sidebyside{\defbox{A graph is \textbf{connected} if there is a path between every pair of vertices.
Otherwise it is \textbf{disconnected}; each connected piece is a \emph{component}.}}{%
\begin{tikzpicture}[scale=0.8]
  \node[v] (a) at (0,0){}; \node[v] (b) at (1.2,0){}; \node[v] (c) at (0.6,1){};
  \draw (a)--(b)--(c)--(a);
  \node[v2] (d) at (2.6,0){}; \node[v2] (e) at (3.6,0.8){};
  \draw (d)--(e);
\end{tikzpicture}\\[-2pt]{\scriptsize Two components}}

\subsection{Complete graph $K_n$: everyone knows everyone}
\kidbox{In a class where every kid is friends with every other kid, each pair gets a line.}
\sidebyside{\defbox{The \textbf{complete graph} $K_n$ has $n$ vertices and every pair is joined by one edge.
It has $\binom{n}{2}=\dfrac{n(n-1)}{2}$ edges. Example: $K_5$ has $\frac{5\cdot4}{2}=10$ edges.}}{%
\begin{tikzpicture}[scale=0.9]
  \foreach \i in {0,...,4}{\node[v] (k\i) at ({90+72*\i}:1.2){};}
  \foreach \i in {0,...,4}{\foreach \j in {0,...,4}{\ifnum\i<\j \draw (k\i)--(k\j);\fi}}
\end{tikzpicture}}

\subsection{Bipartite graph: two teams}
\kidbox{Kids on the left, ice-cream flavours on the right. A line means ``this kid likes this flavour''.
Lines only go \emph{between} the teams, never inside a team.}
\sidebyside{\defbox{A graph is \textbf{bipartite} if $V$ can be split into two disjoint sets $U$ and $W$ so that
every edge joins a vertex of $U$ to a vertex of $W$. Equivalent fact: it has \emph{no odd cycles}.}}{%
\begin{tikzpicture}[scale=0.9]
  \foreach \i in {1,2,3}{\node[v] (u\i) at (0,-0.8*\i+2.4){}; \node[v2] (w\i) at (2,-0.8*\i+2.4){};}
  \draw (u1)--(w1); \draw (u1)--(w2); \draw (u2)--(w2); \draw (u3)--(w2); \draw (u3)--(w3);
  \node[left=1pt of u2,font=\scriptsize] {Kids}; \node[right=1pt of w2,font=\scriptsize] {Flavours};
\end{tikzpicture}}
\realbox{Students and courses, jobs and applicants, doctors and patients.}

\subsection{Planar graph: no crossing lines}
\kidbox{Can you draw it on paper so that no lines cross? Then it's \emph{planar}. Like a clean map.}
\sidebyside{\defbox{A graph is \textbf{planar} if it can be drawn in the plane with no edges crossing.
For a connected planar graph, Euler's formula says $V-E+F=2$ where $F$ counts faces (regions, including the outside).
$K_5$ and $K_{3,3}$ are \emph{not} planar.}}{%
\begin{tikzpicture}[scale=0.9]
  \node[v] (a) at (90:1.3){}; \node[v] (b) at (210:1.3){}; \node[v] (c) at (330:1.3){}; \node[v] (d) at (0,0){};
  \draw (a)--(b)--(c)--(a); \draw (d)--(a); \draw (d)--(b); \draw (d)--(c);
\end{tikzpicture}}
\tryit{This picture has $V=4$, $E=6$, $F=4$ (3 inner triangles + the outside). $4-6+4=2$. \checkmark}

\subsection{Tree and forest}
\kidbox{A family tree, or the folders on your computer. There's one top, it branches out, and
there are \textbf{no loops} --- you can never walk in a circle. A group of separate trees is a forest.}
\sidebyside{\defbox{A \textbf{tree} is a connected graph with no cycles. A tree with $n$ vertices always
has exactly $n-1$ edges. A \textbf{forest} is a graph whose components are all trees.}}{%
\begin{tikzpicture}[scale=0.85,level 1/.style={sibling distance=18mm},level 2/.style={sibling distance=9mm}]
  \node[v] {}
    child {node[v] {} child {node[v] {}} child {node[v] {}}}
    child {node[v] {} child {node[v] {}} child {node[v] {}}};
\end{tikzpicture}}
\realbox{Family trees, file folders, company org charts, decision trees.}

\subsection{Directed acyclic graph (DAG): getting dressed}
\kidbox{Some jobs must come before others: socks before shoes, trousers before belt.
Arrows show ``do this first''. And you can never get stuck in a circle of waiting.}
\sidebyside{\defbox{A \textbf{DAG} is a directed graph with no directed cycle. It can be arranged in a line
so that all arrows point forward (a \emph{topological order}).}}{%
\begin{tikzpicture}
  \node[v] (s) at (0,0.8){Socks}; \node[v] (t) at (0,-0.8){Pants};
  \node[v] (sh) at (2.2,0.8){Shoes}; \node[v] (b) at (2.2,-0.8){Belt};
  \draw[->] (s)--(sh); \draw[->] (t)--(b); \draw[->] (t)--(sh);
\end{tikzpicture}}
\realbox{Course prerequisites, project schedules, ``git'' commit history.}

\subsection{Eulerian graph: draw without lifting your pencil}
\kidbox{Can you trace every line exactly once, without lifting your pencil, and end where you began?
Count the lines at each dot: if \emph{every} dot has an even number, you can!}
\sidebyside{\defbox{A connected graph is \textbf{Eulerian} (has a closed Euler trail) iff \emph{every vertex has even degree}.
It has an Euler \emph{trail} (not necessarily closed) iff exactly 0 or 2 vertices have odd degree.}}{%
\begin{tikzpicture}[scale=0.9]
  \node[v] (m) at (0,0){}; \node[v] (a) at (-1.3,0.9){}; \node[v] (b) at (-1.3,-0.9){};
  \node[v] (c) at (1.3,0.9){}; \node[v] (d) at (1.3,-0.9){};
  \draw (m)--(a)--(b)--(m)--(c)--(d)--(m);
\end{tikzpicture}\\[-2pt]{\scriptsize Bow-tie: degrees 4,2,2,2,2}}
\realbox{\textbf{Königsberg bridges (1736).} Leonhard Euler asked: can you cross all 7 bridges of a town
exactly once? Each of the 4 land areas touched an \emph{odd} number of bridges ($5,3,3,3$), so the answer is
\textbf{no}. This puzzle started all of graph theory!}

\subsection{Hamiltonian graph: visit every place once}
\kidbox{A tourist wants to visit every house exactly once and come home. Euler cares about \emph{lines};
Hamilton cares about \emph{dots}.}
\sidebyside{\defbox{A graph is \textbf{Hamiltonian} if it contains a cycle passing through every vertex exactly once.}}{%
\begin{tikzpicture}[scale=0.9]
  \foreach \i in {0,...,5}{\node[v] (p\i) at ({90-60*\i}:1.2){};}
  \foreach \i in {0,...,5}{\pgfmathtruncatemacro{\n}{mod(\i+1,6)}\draw[hl] (p\i)--(p\n);}
  \draw (p0)--(p3); \draw (p1)--(p4);
\end{tikzpicture}\\[-2pt]{\scriptsize Red cycle visits all 6}}
\realbox{This idea is behind the ``travelling salesman'' problem: delivery routes, circuit-board drilling.}

\subsection{Regular graph: everyone is equal}
\kidbox{Every dot has the same number of lines, like a game where every player plays exactly 3 matches.}
\sidebyside{\defbox{A graph is \textbf{$r$-regular} if every vertex has degree $r$.
The famous Petersen graph is $3$-regular with 10 vertices and 15 edges.}}{%
\begin{tikzpicture}[scale=0.85]
  \foreach \i in {0,...,4}{\node[v] (o\i) at ({90+72*\i}:1.4){}; \node[v2] (i\i) at ({90+72*\i}:0.65){};}
  \foreach \i in {0,...,4}{\pgfmathtruncatemacro{\n}{mod(\i+1,5)}\pgfmathtruncatemacro{\m}{mod(\i+2,5)}
    \draw (o\i)--(o\n); \draw (o\i)--(i\i); \draw (i\i)--(i\m);}
\end{tikzpicture}}

%====================================================================
\section{Graphs Found in Real Life}
%====================================================================
\subsection{Small-world graph: ``six degrees of separation''}
\kidbox{You have friends close to you, and your friends know each other. But \emph{one} friend who lives
in another country is like a magic shortcut. A few shortcuts make the whole world feel small!}
\sidebyside{\defbox{A \textbf{small-world network} has \emph{high clustering} (your friends tend to be friends
with each other) and a \emph{short average path length} (about $\ln n$ steps between any two vertices).
Watts and Strogatz (1998) showed that adding a few random shortcuts to a ring creates this.}}{%
\begin{tikzpicture}[scale=0.85]
  \foreach \i in {0,...,11}{\node[v,minimum size=4mm] (s\i) at ({90-30*\i}:1.4){};}
  \foreach \i in {0,...,11}{\pgfmathtruncatemacro{\n}{mod(\i+1,12)}\draw (s\i)--(s\n);}
  \draw[hl] (s0)--(s6); \draw[hl] (s3)--(s9); \draw[hl] (s2)--(s8);
\end{tikzpicture}\\[-2pt]{\scriptsize Red = shortcuts}}
\realbox{Social networks, brain wiring, power grids. Disease and gossip spread fast because of the shortcuts.}

\subsection{Scale-free graph: a few superstars}
\kidbox{In a school, most kids know a handful of people, but a few ``super-popular'' kids know hundreds.
New kids also tend to befriend the already-popular ones, so the popular get \emph{more} popular.}
\sidebyside{\defbox{A \textbf{scale-free network} has a degree distribution following a power law,
$P(k)\sim k^{-\gamma}$ (often $2<\gamma<3$). The very high-degree vertices are called \textbf{hubs}.
Barab\'asi and Albert (1999) explained this by \emph{preferential attachment}.}}{%
\begin{tikzpicture}[scale=0.8]
  \node[v,minimum size=8mm] (h) at (0,0){}; 
  \node[v] (h1) at (-1.5,0.8){}; \node[v] (h2) at (1.5,0.8){}; \node[v] (h3) at (0,-1.5){};
  \draw (h)--(h1); \draw (h)--(h2); \draw (h)--(h3);
  \foreach \a in {120,160,200}{\node[v,minimum size=3mm] (x\a) at ($(h1)+(\a:0.9)$){}; \draw (h1)--(x\a);}
  \foreach \a in {20,60,-20}{\node[v,minimum size=3mm] (y\a) at ($(h2)+(\a:0.9)$){}; \draw (h2)--(y\a);}
  \foreach \a in {-60,-90,-120}{\node[v,minimum size=3mm] (z\a) at ($(h3)+(\a:0.9)$){}; \draw (h3)--(z\a);}
\end{tikzpicture}}
\realbox{The World Wide Web, airline routes (big hub airports), Twitter followers.
Random failures rarely hurt such networks, but attacking the hubs does.}

\subsection{Case study: Google's PageRank}
\kidbox{Each web page is a dot, and each link is an arrow. A page is important if \emph{important pages link to it}
--- like a kid who is popular because popular kids like them.}
\defbox{PageRank score: $\displaystyle PR(v)=\frac{1-d}{N}+d\sum_{u\to v}\frac{PR(u)}{\ell(u)}$, where $N$ is the number of
pages, $\ell(u)$ the number of links leaving $u$, and $d\approx0.85$.}

%====================================================================
\section{Cheat Sheet}
%====================================================================
\begin{center}
\renewcommand{\arraystretch}{1.25}
\begin{tabular}{@{}p{3.6cm}p{5.4cm}p{5.6cm}@{}}
\hline
\textbf{Type} & \textbf{Remember it as\ldots} & \textbf{Key fact}\\ \hline
Undirected & mutual friendship & $\{u,v\}=\{v,u\}$\\
Directed & following someone & arrows, in/out-degree\\
Weighted & road with km & $w:E\to\mathbb{R}$\\
Complete $K_n$ & everyone knows everyone & $\binom n2$ edges\\
Bipartite & two teams & no odd cycles\\
Planar & no crossings & $V-E+F=2$\\
Tree & family tree & $n-1$ edges, no cycles\\
DAG & getting dressed & no directed cycle\\
Eulerian & pencil never lifts & all degrees even\\
Hamiltonian & visit every house once & cycle through all vertices\\
Regular & everybody equal & all degrees $=r$\\
Small-world & six degrees & clustering + shortcuts\\
Scale-free & superstars & power-law, hubs\\ \hline
\end{tabular}
\end{center}

%====================================================================
\section{Quick Quiz}
%====================================================================
\begin{enumerate}[label=\textbf{Q\arabic*.}]
  \item A graph has 5 vertices and every pair is joined. How many edges? \hfill \emph{(10)}
  \item A tree has 12 vertices. How many edges? \hfill \emph{(11)}
  \item Degrees in a graph are $3,3,2,2,2$. How many edges? \hfill \emph{(sum $=12$, so 6)}
  \item Can a graph have degrees $3,3,3$? \hfill \emph{(No: sum is 9, which is odd.)}
  \item Is a triangle bipartite? \hfill \emph{(No: it is an odd cycle.)}
  \item Which graph type models ``Task A before Task B''? \hfill \emph{(DAG)}
  \item A graph has exactly 2 odd-degree vertices. Euler trail? Euler circuit? \hfill \emph{(trail yes, circuit no)}
\end{enumerate}

\vfill
\begin{center}\small\textit{Further reading: L.~Euler (1736); D.~Watts \& S.~Strogatz, \emph{Nature} 393 (1998);
A.-L.~Barab\'asi \& R.~Albert, \emph{Science} 286 (1999); M.~Newman, \emph{SIAM Review} 45 (2003).}\end{center}
\end{document}
