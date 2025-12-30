# hibernate1
the program of hibernate  using Embeddable for This class does NOT have its own table. Its fields will be embedded inside another entity table.”
//App.java
package com.prathmesh.hibernate2;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class App 
{
    public static void main( String[] args )
    {
        Configuration cfg= new Configuration();
         cfg.configure("hibernate.cfg.xml");
        
        SessionFactory factory =cfg.buildSessionFactory();
        
        Session session=factory.openSession();
        
        Transaction tx=session.beginTransaction();
        
        Address add=new Address();
        
        add.setArea("pragatinagar");
        add.setState("Maharastra");
        
        Student st=new Student();
        
        st.setId(1);
        st.setCity("Baramati");
        st.setName("Prathmesh Pawar");
        st.setAddress(add);
        
        session.save(st);
       
        
        tx.commit();
        
        session.close();
        factory.close();

        System.out.println("Data inserted successfully");
    }
}

//Student.java
package com.prathmesh.hibernate2;

import javax.persistence.Embedded;
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Student {

	@Id
	private int id;
	private String city;
	
	private String name;
	
	@Embedded
	private Address address;
	
	public Student ()
	{
	
	}
	
	
    public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	
	public String getCity() {
		return city;
	}


	public void setCity(String city) {
		this.city = city;
	}
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}


	public Address getAddress() {
		return address;
	}


	public void setAddress(Address address) {
		this.address = address;
	}
	
	
}
//Address.java
package com.prathmesh.hibernate2;

import javax.persistence.Embeddable;

@Embeddable
public class Address {

	 private String area;
	 private String state;
	 
	 public String getArea() {
		return area;
	}
	 public void setArea(String area) {
		 this.area = area;
	 }
	 public String getState() {
		 return state;
	 }
	 public void setState(String state) {
		 this.state = state;
	 }
	 
}
