控制器

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
