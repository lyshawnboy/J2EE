
控制器
package com.ly.student.action;

import java.util.List;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import com.ly.classes.pojo.Classes;
import com.ly.classes.service.ClassesService;
import com.ly.student.pojo.Student;
import com.ly.student.service.StudentService;

@Controller
public class StudentAction {

	@Autowired
	StudentService studentService;
	
	@Autowired
	ClassesService classesService;
	
	@RequestMapping("/showAllStudent")
	public String showAll(HttpServletRequest request,HttpServletResponse response){
		List<Student> list = studentService.showAll();
		
		System.out.println("--------------run it !");
		request.setAttribute("info", list);
		
		return "showStudent";
	}
	
	@RequestMapping("/insertStudent")
	public String insert(int id,String name,String sex,int cid){
		Student student = new Student();
		
		student.setId(id);
		student.setName(name);
		student.setSex(sex);
		student.setCid(cid);
		
		studentService.insert(student);
		return "redirect:showAllStudent.do";
	}
	
	@RequestMapping("/deleteStudent")
	public String delete(int id){
		studentService.delete(id);
		return "redirect:showAllStudent.do";
	}
	
	@RequestMapping("/updateStudent")
	public String update(int id,String name,String sex,int cid){
		Student student = new Student();
		
		student.setId(id);
		student.setName(name);
		student.setSex(sex);
		student.setCid(cid);
		
		studentService.update(student);
		return "redirect:showAllStudent.do";
	}
	
	@RequestMapping("/findOneStudent")
	public String findOne(int id,HttpServletRequest request,HttpServletResponse response){
		List<Student> list1 = studentService.findOne(id);
		List<Classes> list2 = classesService.showAll();
		
		request.setAttribute("info", list1);
		request.setAttribute("infoClass", list2);
		
		return "updateStudent";
	}
}

