# Minimum-Score-Triangulation-of-Polygon

You have a convex n-sided polygon where each vertex has an integer value. You are given an integer array values where values[i] is the value of the ith vertex in clockwise order.

Polygon triangulation is a process where you divide a polygon into a set of triangles and the vertices of each triangle must also be vertices of the original polygon. Note that no other shapes other than triangles are allowed in the division. This process will result in n - 2 triangles.

You will triangulate the polygon. For each triangle, the weight of that triangle is the product of the values at its vertices. The total score of the triangulation is the sum of these weights over all n - 2 triangles.

Return the minimum possible score that you can achieve with some triangulation of the polygon.

class Solution(object):
    def minScoreTriangulation(self, values):
        """
        :type values: List[int]
        :rtype: int
        """
        n = len(values)
        dp = [[0] * n for _ in range(n)]
        
        for l in range(2, n):
            for i in range(n - l):
                j = i + l
                dp[i][j] = float('inf')
                
                for k in range(i + 1, j):
                    cost = values[i] * values[k] * values[j] + dp[i][k] + dp[k][j]
                    dp[i][j] = min(dp[i][j], cost)
        
        return dp[0][n - 1]
