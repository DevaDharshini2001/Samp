# Samp


https://yawarali17.blogspot.com/2021/07/crud-operation-using-adonet-read.html?m=1






https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTlmNDNhYzQtNzkxMi00YzRmLTg4MDgtZmUzMjMyNzBmOTIx%40thread.v2/0?context=%7b%22Tid%22%3a%222567b4c1-b0ed-40f5-aee3-58d7c5f3e2b2%22%2c%22Oid%22%3a%22ed24f99f-3954-4de9-b0de-a2fa19249dc9%22%7d

public ActionResult Create()
        {
            return View();
        }

        [HttpPost]
        public ActionResult Create(EmployeeModel emp)
        {
            int i = db.SaveEmployee(emp);
            if (i > 0)
            {
                return RedirectToAction("Index");
            }
            else
            {
                return View();
            }
        }

Add in Context  Class

 SqlCommand cmd = null;
        public int SaveEmployee(EmployeeModel emp)
        {

            if (emp.EmpId > 0)
            {
                cmd = new SqlCommand("usp_updateUmeshEmployee", con);
                cmd.Parameters.AddWithValue("@empId", emp.EmpId);
            }
            else
            {
                cmd = new SqlCommand("spr_InsertEmployeeDetails", con);
            }

            cmd.CommandType = CommandType.StoredProcedure;
            con.Open();
            cmd.Parameters.AddWithValue("@empname", emp.EmpName);
            cmd.Parameters.AddWithValue("@empsalary", emp.EmpSalary);
            int i = cmd.ExecuteNonQuery();
            con.Close();
            return i;
        }

In Table Write Below Store Proc:    

 CREATE Procedure [dbo].[spr_insertEmployeeDetails]
  @EmpName char(50) ,
  @EmpSalary int
  AS
  BEGIN
  Insert into employeeDetails(empname,empsalary)values(@EmpName,@EmpSalary)
  END







