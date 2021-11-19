# Widest-Path-Routing in Java 
The Program is about the Widest Path Routing Problem which is the problem of find the path between two vertices and designated weighted graph 
/*
This is the program that implement the widest path routing
The widest path routing is a problem of finding a path between
two designated vertices and weighted graph
*/
package com.company;

public class WidestPathRouting {

    //This is a global variable
    
    static final int V = 9;
    
    
    /*
    This method find the vertex with minimum distance value
    from the set of vertices
     */
    int minDistance(int dist[], Boolean sptSet[])
    {
        // Initialize min value
        int min = Integer.MAX_VALUE,min_index = -1;

        for (int i = 0; i < V; i++)
            if (sptSet[i] == false && dist[i] <= min) {
                min = dist[i];
                min_index = i;
            }

        return min_index;
    }


    //This function return the vertex and its widest path routing
    // and to print the constructed distance array
    void printSolution(int dist[], int n)
    {
        System.out.printf("%s\t\t%s","Vertex","Distance from Source");
        System.out.println("");
        for (int i = 0; i < V; i++)
            System.out.println(i + " It's widest path routing\t" + dist[i]);
    }

    // algorithm for a graph represented using adjacency matrix
    // representation
    void widestRoute(int graph[][], int src)
    {
        int dist[] = new int[V];

        Boolean sptSet[] = new Boolean[V];
        for (int i = 0; i < V; i++) {
            dist[i] = Integer.MAX_VALUE;
            sptSet[i] = false;
        }

        dist[src] = 0;

        // Find widest path for all vertices(nodes)
        for (int count = 0; count < V - 1; count++) {

            int u = minDistance(dist, sptSet);
            // Mark the picked vertex as processed
            sptSet[u] = true;

            // Update dist value of the adjacent vertices of the
            // picked vertex.
            for (int j = 0; j < V; j++)

                if (!sptSet[j] && graph[u][j] != 0 &&
                        dist[u] != Integer.MAX_VALUE && dist[u] + graph[u][j] < dist[j])
                    dist[j] = dist[u] + graph[u][j];
        }
        // print the constructed distance array
        printSolution(dist, V);
    }

    public static void main(String[] args) {

        /* Let us create the example graph discussed above */
        int graph[][] = new int[][] {
                { 0, 4, 0, 0, 0, 0, 0, 8, 0 },
                { 4, 0, 8, 0, 0, 0, 0, 11, 0 },
                { 0, 8, 0, 7, 0, 4, 0, 0, 2 },
                { 0, 0, 7, 0, 9, 14, 0, 0, 0 },
                { 0, 0, 0, 9, 0, 10, 0, 0, 0 },
                { 0, 0, 4, 14, 10, 0, 2, 0, 0 },
                { 0, 0, 0, 0, 0, 2, 0, 1, 6 },
                { 8, 11, 0, 0, 0, 0, 1, 0, 7 },
                { 0, 0, 2, 0, 0, 0, 6, 7, 0 } };


        WidestPathRouting main = new WidestPathRouting();
        main.widestRoute(graph, 0);
    }
}
