CSE 512 : PHASE II
GROUP-21
All the below mentioned commands are to be run after the setup is ready with spark and hadoop running:

Run the following commands in the bin folder of hadoop:
------------------------------------------------------
./hadoop fs -put ~/Downloads/datasets/arealm.csv hdfs://master:54310/
./hadoop fs -put ~/Downloads/datasets/zcta510.csv hdfs://master:54310/
./hadoop fs -put ~/Downloads/datasets/zcta510-small.csv hdfs://master:54310/

Run the following command in the spark folder:
----------------------------------------------
./bin/spark-shell --jars <Path for the jar file>


Run these commands on the scala shell after imports for calling the join using cartesian product as part of Task1:
------------------------------------------------------------------------------------------------------------------
import org.datasyslab.geospark.spatialOperator.RangeQuery;
import org.datasyslab.geospark.spatialRDD.PointRDD;
import com.vividsolutions.jts.geom.Envelope;
import com.vividsolutions.jts.geom.GeometryFactory;
import com.vividsolutions.jts.geom.Coordinate;
import org.datasyslab.geospark.spatialOperator.KNNQuery;
import org.datasyslab.geospark.spatialRDD.RectangleRDD;
import org.datasyslab.geospark.spatialOperator.JoinQuery;
val rectangleRDD = new RectangleRDD(sc, "hdfs://master:54310/zcta510-small.csv", 0, "csv", "equalgrid", 11);
val objectRDD = new PointRDD(sc, "hdfs://master:54310/arealm.csv", 0, "csv", "equalgrid", 11);
val joinQuery = new JoinQuery(sc,objectRDD,rectangleRDD);
val resultSize = joinQuery.SpatialJoinQueryUsingCartesianProduct(objectRDD,rectangleRDD).count();
---------------------------------------------------------------------------------------------------------------------

Note: The above join using cartesian product is run by creating the rectangleRDD and pointRDD by using equalgrid. This is done since the creation of object is throwing a NullPointerException as the constructor in the class specifies gridtype to be present.


