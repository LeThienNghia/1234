# 1234
[TestClass]
public class Data_Driven
    {
        public TestContext TestContext { get; set; }
        [DataSource("Microsoft.VisualStudio.TestTools.DataSource.CSV", "|DataDirectory|\\DataCSV.csv", "DataCSV.csv",
            DataAccessMethod.Sequential), 
            DeploymentItem("DataCSV.csv")]

        [TestMethod]
        public void TestMethod4()
        {
            BinaryToDeTest testCode = new BinaryToDeTest();

            string binary = TestContext.DataRow[0].ToString();
            bool isSymmetryActual;

            long sumActual = testCode.BinaryToDe(binary, out isSymmetryActual);

            long sumExpect = (long)Convert.ToDouble(TestContext.DataRow[2].ToString());
            bool isSymmetryExpect = (bool)Convert.ToBoolean(TestContext.DataRow[1].ToString());

            Assert.AreEqual(isSymmetryExpect, isSymmetryActual);
            Assert.AreEqual(sumExpect, sumActual);
        }
    }







  [TestClass]
    public class Data_Driven_Ex
    {
        public TestContext TestContext { get; set; }
        [DataSource("Microsoft.VisualStudio.TestTools.DataSource.CSV", "|DataDirectory|\\DataCSV.csv", "DataCSV.csv", DataAccessMethod.Sequential),
            DeploymentItem("DataCSV.csv")]

        [TestMethod]
        public void TestMethod1()
        {
            BinaryToDeTest testCode = new BinaryToDeTest();

            string binary = TestContext.DataRow[0].ToString();
            bool isSymmetryExpect = (bool)Convert.ToBoolean(TestContext.DataRow[1].ToString());
            long sumExpect = (long)Convert.ToDouble(TestContext.DataRow[2].ToString());
            bool isSymmetryActual;
            long sumActual;
            try
            {
                sumActual = testCode.BinaryToDe(binary, out isSymmetryActual);
            }
            catch
            {
                if(bool.Parse(TestContext.DataRow[3].ToString()))
                {
                    Assert.IsTrue(true);
                    return;
                } else
                {
                    Assert.Fail();
                    return;
                }
            }

            if (!bool.Parse(TestContext.DataRow[3].ToString()))
            {
                Assert.AreEqual(isSymmetryExpect, isSymmetryActual);
                Assert.AreEqual(sumExpect, sumActual);
            }
            else
                Assert.Fail();
        }
    }












    [TestClass]
    public class UnitTest1
    {
        [TestMethod]
        public void TestMethod1()
        {
            BinaryToDeTest testCode = new BinaryToDeTest();
            bool isSymmetryActual;
            long sumActual = testCode.BinaryToDe("1010", out isSymmetryActual);
            long sumExpect = 10;
            bool isSymmetryExpect = false;
            Assert.AreEqual(isSymmetryExpect, isSymmetryActual);
            Assert.AreEqual(sumExpect, sumActual);
        }

        [ExpectedException(typeof(Exception))]
        [TestMethod]
        public void TestMethod2()
        {
            BinaryToDeTest testCode = new BinaryToDeTest();
            bool isSymmetryActual;
            long sumActual = testCode.BinaryToDe("111111111111111111111", out isSymmetryActual);
        }

        [ExpectedException(typeof(Exception))]
        [TestMethod]
        public void TestMethod3()
        {
            BinaryToDeTest testCode = new BinaryToDeTest();
            bool isSymmetryActual;
            long sumActual = testCode.BinaryToDe("2", out isSymmetryActual);
        }
    }




    sbin, isSymmetry,	BinarytoDe,	EX
1010, FALSE, 10, FALSE
111111111111111111111111, TRUE, 7, TRUE
2, , , TRUE
