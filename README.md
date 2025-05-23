import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.function.BiConsumer;
import java.util.function.Consumer;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Tester {

	public static void main(String[] args) {
		List<Employee> list = EmployeeAdder.addDetails();
		Set<Integer> intSet = new HashSet<>();
		Set<String> stringSet = new HashSet<>();

		BiConsumer<Object, Object> biPrint = (key, value) -> System.out.println(key + "->" + value);
		Consumer print = System.out::println;
		/*
		
		// 1. Filter Employees by Gender:
		// - Retrieve a list of all female employees.

		list.stream().filter(a -> a.getGender().equals("Female")).forEach(System.out::println);
		System.out.println("--------");

		// 2. Filter Employees by Age:
		// - Get a list of employees older than 30 years.

		list.stream().filter(a -> a.getAge() > 30).forEach(System.out::println);
		System.out.println("--------");

		// 3. Filter Employees by Salary:
		// - Find employees with a salary greater than $50,000.

		list.stream().filter(a -> a.getSalary() > 50000).forEach(System.out::println);
		System.out.println("--------");
		// 4. Map Employee Names:
		// - Create a list of employee names (Strings).

		List<String> nameList = list.stream().map(a -> a.getName()).collect(Collectors.toList());
		System.out.println(nameList);
		System.out.println("--------");

		// 5. Calculate Average Salary:
		// - Calculate the average salary of all employees.
		double d = list.stream().mapToDouble(Employee::getSalary).average().orElseThrow(null);

		System.out.println("Average Salary: " + d);
		System.out.println("--------");

		// 6. Find Maximum Salary:
		// - Find the employee with the highest salary.

		double highSal = list.stream().mapToDouble(Employee::getSalary).max().orElseThrow(null);

		System.out.println("Highest salary: " + highSal);
		System.out.println("--------");

		// 7.Group Employees by Gender:
		// - Group employees by gender and return
		// a map with gender as the key and a list of employees as the value.

		list.stream().collect(Collectors.groupingBy(Employee::getGender))
				.forEach((a, b) -> System.out.println(a + "->" + b + "\n"));
		System.out.println("--------");

		// 8. Count Male Employees:
		// - Count the number of male employees.

		long maleCount = list.stream().filter(emp -> emp.getGender().equals("Male")).count();
		System.out.println(maleCount);
		System.out.println("--------");

		// 9. Sum of All Salaries:
		// - Calculate the total sum of salaries for all employees.

		double sumOfSal = list.stream().mapToDouble(Employee::getSalary).sum();
		System.out.println(sumOfSal);
		System.out.println("--------");

		// 10. Sort Employees by Name:
		// - Sort the employees by their names in alphabetical order.
		list.stream().sorted(Comparator.comparing(Employee::getName)).forEach(System.out::println);
		System.out.println("--------");

		// 11. Sort Employees by Age:
		// - Sort the employees by age in ascending order.

		list.stream().sorted(Comparator.comparing(Employee::getAge)).forEach(System.out::println);
		System.out.println("--------");

		// 12. Sort Employees by Salary:
		// - Sort the employees by salary in descending order.

		list.stream().sorted(Comparator.comparing(Employee::getSalary).reversed()).forEach(System.out::println);
		System.out.println("--------");

		// 13. Find Oldest Employee:
		// - Find the oldest employee.

		int oldAge = list.stream().mapToInt(Employee::getAge).max().orElseThrow(null);
		System.out.println(oldAge);
		System.out.println("--------");

		// 14. Group Employees by Age:
		// - Group employees into age groups (e.g., 20-30, 31-40, etc.)
		//
		list.stream().collect(Collectors.groupingBy(Employee::getAge))
				.forEach((a, b) -> System.out.println(a + "  " + b));

		list.stream().collect(Collectors.groupingBy((t) -> {
			int age = t.getAge();
			if (age >= 20 && age <= 30) {
				return "20-30";
			} else if (age >= 31 && age <= 40) {
				return "31-40";
			} else {
				return "40+";
			}
		})).forEach((a, b) -> System.out.println(a + "->" + b));

		System.out.println("--------");

		// 15. Find Employees with a Specific Age:
		// - Find all employees who are exactly 35 years old.

		list.stream().filter(k -> k.getAge() == 35).forEach(System.out::println);

		// 16. Calculate the Sum of Salaries by Gender:
		// - Calculate the sum of salaries for each gender (i.e., male and female)
		// and return a map with gender as the key and the sum of salaries as the value.

		list.stream().collect(Collectors.groupingBy(Employee::getGender, Collectors.summingDouble(Employee::getSalary)))
				.forEach((a, b) -> System.out.println(a + " -> " + b));

		list.stream().collect(Collectors.groupingBy(Employee::getAge, Collectors.summingDouble(Employee::getSalary)))
				.forEach((a, b) -> System.out.println(a + "->" + b));
		System.out.println("------");

		// 17. Find Employees with Names Starting with "J":
		// - Find all employees whose names start with the letter "E."
		list.stream().filter(a -> a.getName().startsWith("E")).forEach(System.out::println);
		list.stream().filter(a -> a.getName().startsWith("B")).forEach(System.out::println);
		System.out.println("-----------");

		// 18. Calculate the Average Salary for Male and Female Employees:
		// - Calculate the average salary separately for male
		// and female employees and return a map with gender
		// as the key and the average salary as the value.

		list.stream()
				.collect(Collectors.groupingBy(Employee::getGender, Collectors.averagingDouble(Employee::getSalary)))
				.forEach((gender, averageSal) -> System.out.println(gender + "-->" + averageSal));
		System.out.println("-------");

		// 19. Find the Top N Highest Paid Employees:
		// - Find the top N employees with the highest salaries.
		list.stream().sorted((a, b) -> a.getSalary() > b.getSalary() ? -1 : 0).limit(5).forEach(System.out::println);
		System.out.println("--------");

		// 20. Retrieve Distinct Age Values:
		// - Get a list of distinct ages of all employees.

		IntStream six = list.stream().mapToInt(a -> a.getAge()).distinct();

		six.forEach(System.out::println);

		list.stream().filter(k -> !intSet.add(k.getAge())).forEach(System.out::println);

		System.out.println("=================");

		// 21. Find the Three Lowest-Paid Employees:
		// - Find and display the names of the three employees with the lowest salaries.

		list.stream().sorted((a, b) -> a.getSalary() > b.getSalary() ? 1 : 0).limit(3).forEach(System.out::println);
		System.out.println("-------");

		// 22. Sort Employees by Name Length:
		// - Sort employees by the length of their names (shortest to longest).

		list.stream().sorted((a, b) -> a.getName().length() > b.getName().length() ? 1 : -1)
				.forEach(System.out::println);
		System.out.println("-------");

		// 23. Group Employees by Age Range:
		// - Group employees into custom
		// age ranges (e.g., 20-29, 30-39, etc.) and
		// return a map with the age range as the key and a list of employees as the
		// value.

		list.stream().collect(Collectors.groupingBy((t) -> {
			int age3 = t.getAge();
			if (age3 >= 20 && age3 <= 29) {
				return "20-29";
			} else if (age3 >= 30 && age3 <= 39) {
				return "30-39";
			} else {
				return "40+";
			}
		})).forEach((a, emp) -> System.out.println(a + " -->" + emp));
		System.out.println("-----");

		// 24. Find the Average Salary of Employees Aged 30 or Younger:
		// - Calculate the average salary of employees aged 30 or younger.

		double avgsalAbove30 = list.stream().filter(age -> age.getAge() <= 30).mapToDouble(a -> a.getSalary()).average()
				.orElseThrow(null);
		System.out.println(avgsalAbove30);
		System.out.println("----------------");

		// 25. Find the Names of Male Employees with Salaries Over $60,000:
		// - Retrieve the names of male employees with salaries over $60,000.
		
		list.stream().filter(e -> e.getSalary() >= 53000 && e.getGender().equals("Male")).map(k -> k.getName())
				.forEach(System.out::println);

		// 26. Find the Youngest Female Employee:
		// - Find the youngest female employee.
		list.stream().filter(a -> a.getGender().equals("Female")).sorted((a, b) -> a.getAge() > b.getAge() ? 1 : -1)
				.limit(1).forEach(System.out::println);

		// 27. Retrieve the Names of Employees in Reverse Order:
		// - Get a list of employee names in reverse order (from the last employee to
		// the first).

		List<String> listOfNames = list.stream().map(k -> k.getName()).collect(Collectors.toList());

		Collections.reverse(listOfNames);
		System.out.println(listOfNames);
		System.out.println("-----");

		// 28. Find the Highest Salary Among Female Employees:
		// - Find the highest salary among female employees.
		list.stream().filter(a -> a.getGender().equals("Female"))
				.sorted((a, b) -> a.getSalary() > b.getSalary() ? -1 : 1).limit(1).forEach(System.out::println);
		System.out.println("----");

		// 29. Group Employees by Age and Gender:
		// - Group employees by both age and gender and return a multi-level map.
		Map<String, Map<Integer, List<Employee>>> multiLevMap = list.stream()
				.collect(Collectors.groupingBy(Employee::getGender, Collectors.groupingBy(Employee::getAge)));

		multiLevMap.forEach((key, value) -> {
			System.out.println(key + "---->" + value);
			value.forEach((k, v) -> System.out.println(k + "<-->" + v));
		});
		System.out.println("-----");

		// 30. Find the Sum of Salaries for Employees with Names Containing "Ojha":
		// - Calculate the sum of salaries for employees whose names contain the
		// substring "Smith."

		double sumOfSmiith = list.stream().filter(a -> a.getName().contains("Ojha")).mapToDouble(Employee::getSalary)
				.sum();
		System.out.println(sumOfSmiith);
		System.out.println("===============");

		// 31. Find the Names of Employees Aged 30-40 with Salaries Between $50,000 and
		// $60,000:
		// - Retrieve the names of employees aged 30-40 with salaries between $50,000
		// and $60,000.

		list.stream().filter(
				p -> (p.getAge() >= 30 && p.getAge() <= 40) && (p.getSalary() >= 50000 && p.getSalary() <= 60000))
				.forEach(System.out::println);
		System.out.println("-");

		// 32. Calculate the Total Number of Employees:
		// - Determine the total count of employees.

		long totalEmployee = list.stream().count();
		System.out.println(totalEmployee);
		System.out.println("--");

		// 33. Find the Most Common Age Among Employees:
		// - Determine the age that is most common among the employees.

		double avgAge = list.stream().mapToInt(Employee::getAge).average().orElseThrow(null);
		System.out.println(avgAge);

		// 34. Find the Median Salary:
		// - Calculate the median salary of all employees.
		
		List<Employee> medianSal=list.stream().sorted(Comparator.comparing(Employee::getSalary)).collect(Collectors.toList());
		int size=medianSal.size();
		double res;
		if(size%2!=0) {
			 res=medianSal.get(size/2).getSalary();
		}else {
			res=(medianSal.get(size/2-1).getSalary()+medianSal.get(size/2).getSalary())/2;
		}
		
		System.out.println(res);
		System.out.println("++++++34+++++++");

		// 35. Group Employees by Age and Count:
		// - Group employees by age and count the number of employees in each age group.

		list.stream().collect(Collectors.groupingBy(Employee::getAge, Collectors.counting()))
				.forEach((a, b) -> System.out.println(a + "-->" + b));
		System.out.println("-----");

		// 36. Find the Employee with the Longest Name:
		// - Find the employee with the longest name.

		list.stream().sorted((a, b) -> a.getName().length() > b.getName().length() ? -1 : 1).limit(1)
				.forEach(System.out::println);
		System.out.println("------");

		// 37. Calculate the Sum of Salaries for Each Age:
		// - Calculate the sum of salaries for each distinct age in a map.

		list.stream().collect(Collectors.groupingBy(Employee::getAge, Collectors.summingDouble(Employee::getSalary)))
				.forEach((key, value) -> System.out.println(key + " -->" + value));
		System.out.println("-------");

		// 38. Sort Employees by Age, Then by Salary:
		// - Sort employees first by age in ascending order, and then by salary in
		// descending order.
		

		// This is wrong logic because in stream last sorted overrides the before sorted
		// operations
		// list.stream().sorted((a,b)->b.getAge()-a.getAge()).sorted((a,b)->(int)(a.getSalary()-b.getSalary())).forEach(System.out::println);

		list.stream()
				.sorted(Comparator.comparing(Employee::getAge)
						.thenComparing(Comparator.comparing(Employee::getSalary).reversed()))
				.forEach(System.out::println);
		System.out.println("--------");

		// 39. Find Employees Whose Names Contain More Than One Word:
		// - Retrieve employees whose names consist of more than one word.

		list.stream().filter(a -> a.getName().trim().contains(" ")).forEach(System.out::println);
		System.out.println("---------");

		// 40. Find the Two Highest Paid Female Employees:
		// - Find and display the names of the two highest-paid female employees.
		// Approach 1
		list.stream().sorted(Comparator.comparing(Employee::getSalary).reversed()).limit(2)
				.forEach(System.out::println);
		System.err.println("====");

		// Approach 2
		list.stream().sorted((a, b) -> (int) (b.getSalary() - a.getSalary())).limit(2).forEach(System.out::println);
		System.err.println("====");

		// Appraoch 3
		list.stream().sorted((a, b) -> a.getSalary() > b.getSalary() ? -1 : 1).limit(2).forEach(System.out::println);
		System.err.println("===========");

		// 41. Find the Employee with the Highest Salary in Each Gender:
		// - Find the employee with the highest salary for each gender (male and
		// female).

		// Approach 1
		list.stream().sorted(Comparator.comparing(Employee::getSalary).reversed()).limit(2)
				.collect(Collectors.groupingBy(Employee::getGender))
				.forEach((k, v) -> System.out.println(k + "-->" + v));

		// Approach 2
		list.stream()
				.collect(
						Collectors.toMap(Employee::getGender, k -> k, (a, b) -> a.getSalary() >= b.getSalary() ? a : b))
				.forEach((k, v) -> System.out.println(k + "--->" + v));
		System.out.println("-");

		// 42. Retrieve Employees with Unique Names:
		// - Find employees with unique names (no duplicate names in the list).

		list.stream().map(a -> a.getName()).distinct().forEach(System.out::println);
		System.out.println("--");

		// 43. Find the Names of Employees in Uppercase:
		// - Get a list of employee names in uppercase.

		list.stream().filter(a -> a.getName().equals(a.getName().toUpperCase())).forEach(System.out::println);
		System.out.println("---");

		// 44. Calculate the Salary Range (Min-Max) for Each Age Group:
		// - Calculate the salary range (minimum and maximum) for each distinct age
		// group.
		
		System.err.println("===44===");
		list.stream().
		collect(Collectors.groupingBy(Employee::getAge,
				Collectors.collectingAndThen(Collectors.toList(),employees->{
					double min=employees.stream().mapToDouble(Employee::getSalary).min().orElseThrow(()->new RuntimeException(""));
					double max=employees.stream().mapToDouble(Employee::getSalary).max().orElseThrow(()->new RuntimeException(""));
					
					Map<String,Double> map=new HashMap<>();
					map.put("min", min);
					map.put("max",max);
					return map;
				}))).forEach((age,salary)->System.out.println("Age is:"+age+"Min Salary : "+salary.get("min")+"Max Salary : "+salary.get("max")));
		
		System.err.println("======");
		
		
		

		// 45. Filter Employees by First Name Initial:
		// - Retrieve employees whose first name starts with a specific initial (e.g.,
		// 'A').

		list.stream().filter(a -> a.getName().startsWith("S")).forEach(System.out::println);
		System.out.println("-----");

		// 46. Group Employees by Age and List Only Unique Salaries:
		// - Group employees by age and display a list of unique salaries for each age
		// group.

		list.stream()
				.collect(Collectors.groupingBy(Employee::getAge,
						Collectors.mapping(Employee::getSalary, Collectors.toSet())))
				.forEach((k, v) -> System.out.println(k + "-->" + v));
		System.out.println("------");

		// 47. Find Employees with the Same Salary:
		// - Identify and display employees who have the same salary.

		list.stream().collect(Collectors.groupingBy(e -> e.getSalary())).entrySet().stream()
				.filter(p -> p.getValue().size() > 1).forEach(k -> {
					System.out.println(k.getKey());
					k.getValue().forEach(System.err::println);
				});
		System.out.println("-------");

		// 48. Find the Employee with the Shortest Name Among Male Employees:
		// - Find the male employee with the shortest name.

		// Approach 1
		list.stream().sorted((a, b) -> a.getName().length() > b.getName().length() ? 1 : -1)
				.filter(a -> a.getGender().equals("Male")).limit(1).forEach(System.out::println);

		// Approach 2
		System.out.println();
		Employee minName = list.stream().filter(a -> a.getGender().equals("Male"))
				.min((a, b) -> a.getName().length() > b.getName().length() ? 1 : -1).orElseThrow(null);

		System.out.println(minName);
		System.out.println("--------");

		// 49. Find the Most Common Salary Value:
		// - Determine the salary value that appears most frequently among the
		// employees.

		double commonSal = list.stream().collect(Collectors.groupingBy(Employee::getSalary, Collectors.counting()))
				.entrySet().stream().max(Map.Entry.comparingByValue()).map(Map.Entry::getKey)
				.orElseThrow(() -> new RuntimeException("Common salary not found"));

		System.out.println("Common Salary is: " + commonSal);
		System.out.println("---------");

		// 50. Find the Oldest Employee with the Lowest Salary:
		// - Find the oldest employee with the lowest salary.

		Employee oldLowestsalEmp = list.stream()
				.filter(k -> k.getAge() == list.stream().mapToInt(Employee::getAge).max()
						.orElseThrow(() -> new RuntimeException("No Old emp found")))
				.min(Comparator.comparingDouble(Employee::getSalary)).get();
		System.out.println("OldLowestSalary Employee is: " + oldLowestsalEmp);

		System.err.println("----------");

		// 51. Filter Employees by Gender:
		// - Retrieve a list of all female employees.

		list.stream().filter(a -> a.getGender().equals("Female")).forEach(System.out::println);
		System.out.println(" ");

		// 52. Filter Employees by Age:
		// - Get a list of employees older than 30 years.

		list.stream().collect(Collectors.groupingBy(Employee::getAge)).forEach(biPrint);
		System.out.println("--");
		// 53. Filter Employees by Salary:
		// - Find employees with a salary greater than $50,000.

		list.stream().filter(p -> p.getSalary() >= 50000).forEach(print);
		System.out.println("---");

		// 54. Map Employee Names:
		// - Create a list of employee names (Strings).

		list.stream().map(Employee::getName).collect(Collectors.toList()).forEach(print);
		System.out.println("----");

		// 55. Calculate Average Salary:
		// - Calculate the average salary of all employees.

		double avgSalary = list.stream().mapToDouble(Employee::getSalary).average()
				.orElseThrow(() -> new RuntimeException("average not found"));
		System.out.println("Average salary is: " + avgSalary);
		// 56. Find Maximum Salary:
		// - Find the employee with the highest salary.

		double maxSalary = list.stream().mapToDouble(Employee::getSalary).max()
				.orElseThrow(() -> new RuntimeException("salary not found"));

		System.out.println("Max Salary is: " + maxSalary);
		System.out.println("------");

		// 57. Group Employees by Gender:
		// - Group employees by gender
		// and return a map with gender as the key and a list of employees as the value.

		list.stream().collect(Collectors.groupingBy(Employee::getGender)).forEach(biPrint);
		System.out.println("-------");

		// 58. Count Male Employees:
		// - Count the number of male an female employees.
		long maleCount1 = list.stream().filter(p -> p.getGender().equals("Female")).count();
		System.out.println(maleCount1);
		System.out.println("--------");

		// 59. Sum of All Salaries:
		// - Calculate the total sum of salaries for all employees.

		double sumOfSal1 = list.stream().mapToDouble(Employee::getSalary).sum();
		System.out.println("Sum Of Salary is: " + sumOfSal1);
		System.out.println("---------");

		// 60. Sort Employees by Name:
		// - Sort the employees by their names in alphabetical order.

		list.stream().sorted(Comparator.comparing(Employee::getName)).forEach(print);
		System.err.println("----------");

		// 61. Find the Employee with the Highest Salary in Each Gender:
		// - Find the employee with the highest salary for each gender (male and
		// female).
		list.stream()
				.collect(Collectors.toMap(Employee::getGender, t -> t, (t, u) -> t.getSalary() > u.getSalary() ? t : u))
				.forEach(biPrint);
		System.out.println("-");

		// 62. Retrieve Employees with Unique Names:
		// - Find employees with unique names (no duplicate names in the list).

		list.stream().map(name -> name.getName()).distinct().forEach(print);
		System.out.println("--");

		// 63. Find the Names of Employees in Uppercase:
		// - Get a list of employee names in uppercase.

		list.stream().filter(p -> p.getName().equals(p.getName().toUpperCase())).forEach(print);
		System.out.println("---");

  */
		// 64. Calculate the Salary Range (Min-Max) for Each Age Group:
		// - Calculate the salary range (minimum and maximum) for each distinct age
		// group.
		
		
		
		list.stream().collect(Collectors.groupingBy(Employee::getAge,Collectors.collectingAndThen(Collectors.toList(), emp->{
			double min=emp.stream().mapToDouble(Employee::getSalary).min().orElseThrow(()->new RuntimeException(""));
			double max=emp.stream().mapToDouble(Employee::getSalary).max().orElseThrow(()->new RuntimeException(""));
			
			Map<String,Double> map=new HashMap<>();
			map.put("min",min);
			map.put("max",max);
			return map;
			
		}))).forEach((age,sal)->System.out.println("age :"+age+" "+"min sal:"+sal.get("min")+" "+sal.get("max")));

		
		
		// 65. Filter Employees by First Name Initial:
		// - Retrieve employees whose first name starts with a specific initial (e.g.,
		// 'E').

		list.stream().filter(name -> name.getName().startsWith("S")).forEach(print);
		System.out.println("-----");

		// 66. Group Employees by Age and List Only Unique Salaries:
		// - Group employees by age and display a list of unique salaries for each age
		// group.

		list.stream().collect(
				Collectors.groupingBy(Employee::getAge, Collectors.mapping(Employee::getSalary, Collectors.toSet())))
				.forEach(biPrint);

		System.out.println("------");
		// 67. Find Employees with the Same Salary:
		// - Identify and display employees who have the same salary.

		list.stream().collect(Collectors.groupingBy(Employee::getSalary)).entrySet().stream()
				.filter(k -> k.getValue().size() > 1)
				.forEach(t -> System.out.println(t.getKey() + "-->" + t.getValue()));

		System.out.println("-------");
		// 68. Find the Employee with the Shortest Name Among Male Employees:
		// - Find the male employee with the shortest name.

		// Approach 1
		list.stream().filter(name -> name.getGender().equals("Male"))
				.sorted((a, b) -> a.getName().length() > b.getName().length() ? 1 : -1).limit(1).forEach(print);

		// Approach 2
		Employee emp1 = list.stream().filter(name -> name.getGender().equals("Male"))
				.min((a, b) -> a.getName().length() > b.getName().length() ? 1 : -1)
				.orElseThrow(() -> new RuntimeException("Employee Not found"));
		System.out.println(emp1);

		System.out.println("--------");
		// 69. Find the Most Common Salary Value:
		// - Determine the salary value that appears most frequently among the
		// employees.

		double commonSalary = list.stream().collect(Collectors.groupingBy(Employee::getSalary, Collectors.counting()))
				.entrySet().stream().max(Map.Entry.comparingByValue()).map(Map.Entry::getKey).get();

		System.out.println(commonSalary);

		System.out.println("---------");

		// 70. Find the Oldest Employee with the Lowest Salary:
		// - Find the oldest employee with the lowest salary.

		Employee oldestSalary = list.stream()
				.filter(p -> p.getAge() == list.stream().mapToInt(Employee::getAge).max()
						.orElseThrow(() -> new RuntimeException("Age not found")))
				.min(Comparator.comparingDouble(Employee::getSalary)).get();

		System.out.println(oldestSalary);
		System.err.println("----------");

		// 71. Find the Most Common Age Among Employees:
		// - Determine the age that is most common among the employees.

		int commonAge = list.stream().collect(Collectors.groupingBy(Employee::getAge, Collectors.counting())).entrySet()
				.stream().max(Map.Entry.comparingByValue()).map(Map.Entry::getKey).get();

		System.out.println("Common age is: " + commonAge);

		System.out.println("-");

		// 72. Find the Employee with the Longest Name:
		// - Find the employee with the longest name.

		list.stream().sorted((a, b) -> a.getName().length() > b.getName().length() ? -1 : 1).limit(1).forEach(print);
		System.out.println("--");

		// 73. Find Employees with Palindromic Names:
		// - Retrieve employees whose names are palindromes (e.g., "Anna" or "Bob").

		list.stream().filter(k -> {
			String mainString = k.getName().toLowerCase();
			StringBuffer sb = new StringBuffer(mainString);
			return mainString.contentEquals(sb.reverse());
		}).forEach(print);
		System.out.println("---");

		// 74. Calculate the Sum of Salaries for Employees with Odd Ages:
		// - Calculate the sum of salaries for employees with odd ages.

		double sumOfSalaryOddAged = list.stream().filter(a -> a.getAge() % 2 != 0).mapToDouble(Employee::getSalary)
				.sum();
		System.out.println("Sum of salary of odd age Guys: " + sumOfSalaryOddAged);
		System.out.println("----");

		// 75. Find the Employee with the Highest Salary Whose Name Contains "Smith":
		// - Find the employee with the highest salary whose name contains the word
		// "Smith."

		Employee emp3 = list.stream().filter(name -> name.getName().contains("Jyoti"))
				.max(Comparator.comparing(Employee::getSalary)).get();
		System.out.println(emp3);
		System.out.println("-----");

		// 76. Group Employees by the First Letter of Their Names:
		// - Group employees by the first letter
		// of their names and return a map with
		// the letter as the key and a list of employees as the value.

		list.stream().collect(Collectors.groupingBy(s -> s.getName().charAt(0))).forEach(biPrint);
		System.out.println("------");

		// 77. Find the Employee with the Shortest Name:
		// - Find the employee with the shortest name.

		Employee emp4 = list.stream()
				.min((name1, name2) -> name1.getName().length() > name2.getName().length() ? 1 : -1).get();

		System.out.println("Employee with shortest name: " + emp4);
		System.out.println("-------");

		// 78. Calculate the Average Salary of Employees Whose Names Start with "E":
		// - Calculate the average salary of employees whose names start with the letter
		// "E."

		double avgSalOfE = list.stream().filter(p -> p.getName().startsWith("E")).mapToDouble(Employee::getSalary)
				.average().getAsDouble();

		System.out.println(avgSalOfE);
		System.out.println("--------");

		// 79. Filter Employees by Age Range:
		// - Filter employees
		// based on a custom age range (e.g., between 25 and 35 years old).

		list.stream().filter(p -> p.getAge() >= 25 && p.getAge() <= 35).forEach(print);
		System.out.println("---------");

		// 80. Group Employees by the First Two Letters of Their Names:
		// - Group employees by the first two letters
		// of their names and
		// return a map with the letters as the key and a list of employees as the
		// value.

		list.stream().collect(Collectors.groupingBy(k -> k.getName().substring(0, 2))).forEach(biPrint);

		System.err.println("----------");

		// 81. Find the Employee with the Longest Name Whose Salary Is Below $70,000:
		// - Find the employee with the longest name whose salary is below $70,000.

		Employee emp5 = list.stream().filter(sal -> sal.getSalary() <= 70000)
				.max((name1, name2) -> name1.getName().length() > name2.getName().length() ? 1 : -1).get();

		System.out.println(emp5);
		System.out.println("-");

		// 82. Calculate the Average Salary of Employees Whose Names End with "son":
		// - Calculate the average salary of employees whose names end with the suffix
		// "son."

		double avgSalOfOjha = list.stream().filter(name -> name.getName().toLowerCase().endsWith("ojha"))
				.mapToDouble(Employee::getSalary).average().getAsDouble();

		System.out.println(avgSalOfOjha);
		System.out.println("--");

		// 83. Group employees by the number of
		// words in their names (e.g., one-word names, two-word names, etc.)
		// and return a map with the count as the key and a list of employees as the
		// value.

		list.stream().collect(Collectors.groupingBy(p -> p.getName().length())).forEach(biPrint);
		System.out.println("---");
		// 84. Calculate the Average Salary of Employees Whose Names Contain Both "S"
		// and "O":
		// - Calculate the average salary of employees whose names contain both the
		// letters "A" and "E."

		double avgOfTwo = list.stream()
				.filter(name -> name.getName().toUpperCase().contains("S")
						&& name.getName().toUpperCase().contains("H"))
				.mapToDouble(Employee::getSalary).average().getAsDouble();
		System.out.println(avgOfTwo);
		System.err.println("--------End-----------");
	}

}










//student interview question


import java.util.Arrays;
import java.util.List;
import java.util.Optional;
import java.util.function.Consumer;
import java.util.stream.Collectors;

public class StreamAPIInterviewQuestion {

	public static void main(String[] args) {
		
		List<String> stringList=Arrays.asList("subrat","dipu","satya","deba");
		List<Integer> list=Arrays.asList(1,2,3,4,5,6,5,4,15);
		Consumer print=System.out::println;
	//	1.Write a program to find the sum of all elements in a list using Java Stream API
	
		int sumOfEle=list.stream().mapToInt(Integer::intValue).sum();

		System.out.println(sumOfEle);
	
	//	2. Given a list of integers, write a program to find and print the maximum element using Java Stream API
		  Optional<Integer> maxNo=list.stream().max((a,b)->Double.compare(a,b));
		System.out.println(maxNo.get());
		
			
	//	3. Write a program to filter out all the even numbers from a list using Java Stream API
		
		list.stream().filter(k->k%2==0).forEach(System.out::println);
		
	
	//	4. Given a list of strings, write a program to count the number of strings containing a specific character ‘a’ using Java Stream API.
		long countSpec=stringList.stream().filter(a->a.contains("a")).count();
		System.out.println(countSpec);
		
	
	//	5. Write a program to convert a list of strings to uppercase using Java Stream API.
		
		stringList.stream().map(k->k.toUpperCase()).forEach(System.out::println);
				
		
    //	6. Given a list of integers, write a program to calculate the average of all the numbers using Java Stream API.
			
		double avgOfList=list.stream().mapToInt(Integer::intValue).average().getAsDouble();
		System.out.println(avgOfList);
		
		
	
	//	7. Write a program to sort a list of strings in alphabetical order using Java Stream API.
		
		stringList.stream().sorted().forEach(System.out::println);
			
	//	8. Given a list of strings, write a program to concatenate all the strings using Java Stream API.
		
		String concatString=stringList.stream().collect(Collectors.joining());
		
		System.out.println("Concat String is: "+concatString);
		

		
	//	9. Write a program to find the longest string in a list of strings using Java Stream API.
		
		stringList.stream().max((a,b)->a.length()>b.length()?1:-1).ifPresent(System.out::println);
			
	//	10. Given a list of integers, write a program to find and print the second largest number using Java Stream API.
		
		list.stream().sorted((a,b)->b-a).limit(2).skip(1).forEach(System.out::println);

		
		
	//	11. Write a program to remove all the duplicate elements from a list using Java Stream API.
		
		list.stream().distinct().forEach(System.out::println);
			
		
	//	12. Given a list of strings, write a program to find and print the shortest string using Java Stream API.
		
		stringList.stream().sorted().limit(1).forEach(print);
			
		
	//	13. Write a program to convert a list of integers to a list of their squares using Java Stream API.
		
		list.stream().map(a->a*a).forEach(print);
	
		
	//	14. Given a list of strings, write a program to find and print the strings starting with a specific prefix ‘a’ using Java Stream API.
		
		stringList.stream().filter(a->a.startsWith("s")).forEach(print);
			
	//	15. Write a program to find the product of all elements in a list of integers using Java Stream API.
			
		int prodvalue=list.stream().reduce(1,(a,b)->a*b);
		System.out.println("Product is: "+prodvalue);
	
		
	//	16. Given a list of integers, write a program to find and print the prime numbers using Java Stream API.
		
		list.stream().filter(StreamAPIInterviewQuestion::isPrime).forEach(print);
		
			
		
	//	17. Write a program to check if a list of strings contains a specific string using Java Stream API.
		
		stringList.stream().filter(a->a.contains("satya")).forEach(print);
		
	//	18. Given a list of strings, write a program to find and print the strings with length greater than a specified value 5 using Java Stream API.
		
		stringList.stream().filter(a->a.length()>4).forEach(print);
		
	
	//	19. Write a program to filter out all the elements divisible by 3 and 5 from a list of integers using Java Stream API.
		
		list.stream().filter(a->a%3==0 && a%5==0).forEach(print);
		
		
	//	20. Given a list of strings, write a program to find and print the strings with the maximum length using Java Stream API.
		
		stringList.stream().sorted((a,b)->b.length()-a.length()).forEach(print);
		
		
	}
	
	private static boolean isPrime(int n) {
		if(n<=1) {
			return false;
		}
		
		for(int i=2;i<=Math.sqrt(n);i++) {
			if(n%i==0)
			{
				return false;
			}
		}
		
		return true;
	}

 //	//21. Write a program to reverse a list of strings using Java Stream API.
//	
//	
//		
//       Collections.reverse(stringList);
//       System.out.println(stringList);
//	List<String> reversedList=IntStream.range(0,stringList.size())
//			.mapToObj(i->stringList.get(stringList.size()-1-i))
//			.collect(Collectors.toList());
	
	
	
//	//22. Given a list of integers, write a program to find and print the distinct odd numbers using Java Stream API.
//
//		list.stream().filter(a->a%2!=0).distinct().forEach(print);
//		
//	//23. Write a program to remove all null values from a list of strings using Java Stream API.
//	
//		stringList.stream().filter(a->a!=null).forEach(print);
//		
//	//24. Given a list of integers, write a program to find and print the sum of all odd numbers using Java Stream API.
//	
//		int sumOfOdd=list.stream().filter(a->a%2!=0).mapToInt(Integer::intValue).sum();
//		System.out.println(sumOfOdd);
	//25. Write a program to find the intersection of two lists of strings using Java Stream API.
	
		List<String> f=Arrays.asList("a","c","e","g");
		List<String> s=Arrays.asList("b","a","f","e");
//		//approach 1
//		f.stream().filter(a->s.contains(a)).forEach(print);
//		//approach 2
//		f.stream().filter(s::contains).forEach(System.out::println);
//		
	//26. Given a list of strings, write a program to find and print the strings containing only vowels using Java Stream API.
	
//		//approach 1
//		f.stream().filter(a->a.equals("a")|| a.equals("e")|| a.equals("i")|| a.equals("o")|| a.equals("u") ).forEach(print);
//		
//		System.out.println("----");
//		//approach2
//		s.stream().filter(a->a.matches("[aeiouAEIOU]+")).forEach(print);
	//27. Write a program to convert a list of strings to a comma-separated string using Java Stream API.
	
//		String joinString=f.stream().collect(Collectors.joining(","));
//		System.out.println(joinString);
//	//28. Given a list of integers, write a program to find and print the index of the first occurrence of a specific number using Java Stream API.
//	
//		int index=8;
//		list.stream().filter(a->a.equals(list.get(8))).forEach(print);
//	//29. Write a program to find the union of two lists of integers using Java Stream API.
//	       List<Integer> al=Arrays.asList(1,2,3,4,5,6);
//	       List<Integer> bl=Arrays.asList(5,6,7,8,9);
//	      
//	       Stream.concat(al.stream(),bl.stream()).distinct().forEach(print);
	       
//	//30. Given a list of strings, write a program to find and print the strings containing duplicate characters using Java Stream API.
//	
//		stringList.stream().filter(a->a.length()!=a.chars().distinct().count()).forEach(print);
		
	//31. Write a program to check if all elements in a list of strings are of the same length using Java Stream API.
	
		boolean sameLength=stringList.stream().map(a->a.length()).distinct().count()==1;
		System.out.println("All element are same in list  :"+sameLength);
	//32. Given a list of integers, write a program to find and print the difference between the maximum and minimum numbers using Java Stream API.
	
	//33. Write a program to remove all whitespace from a list of strings using Java Stream API.
	
	//34. Given a list of strings, write a program to find and print the strings containing a specific substring using Java Stream API.
	
	//35. Write a program to find the mode of a list of integers using Java Stream API.
	
	//36. Given a list of strings, write a program to find and print the strings with the minimum length using Java Stream API.
	
	//37. Write a program to find the frequency of each element in a list of integers using Java Stream API.
	
	//38. Given a list of strings, write a program to find and print the strings with the maximum number of vowels using Java Stream API.
	
	//39. Write a program to check if a list of integers is sorted in ascending order using Java Stream API.
	
	//40. Given a list of strings, write a program to find and print the strings with the minimum number of vowels using Java Stream API.
	
	//41. Write a program to find the median of a list of integers using Java Stream API.
	
	//42. Given a list of strings, write a program to find and print the strings containing a specific character at least twice using Java Stream API.
	
	//43. Write a program to find the kth smallest element in a list of integers using Java Stream API.
	
	//44. Given a list of strings, write a program to find and print the strings with the maximum number of consonants using Java Stream API.
	
	//45. Write a program to check if a list of strings is palindrome using Java Stream API.
	
	//46. Given a list of integers, write a program to find and print the elements with the highest frequency using Java Stream API.
	
	//47. Write a program to remove all non-numeric characters from a list of strings using Java Stream API.
	
	//48. Given a list of strings, write a program to find and print the strings containing only digits using Java Stream API.
	
	//49. Write a program to find the kth largest element in a list of integers using Java Stream API.
	
	//50. Given a list of integers, write a program to find and print the elements with the lowest frequency using Java Stream API.


 Are you preparing for a Java developer interview? The Stream API is a frequent topic in technical interviews, known for its ability to process collections of data elegantly. In this article, I’ll walk you through 15 real interview questions that will help you master Java Streams.

Problem 1: Write a Program to find the Maximum element in an array?
int arr[] = {5,1,2,8};
Arrays.stream(arr).max().getAsInt();
Problem 2: Write a program to print the count of each character in a String?
String str = "Now is the winter";
Map<String, Long> charFreq = Arrays.stream(str.split(""))
    .collect(Collectors.groupingBy(
        Function.identity(), // or x -> x
        Collectors.counting()
    ));
Problem 3: Merge two arrays of Person objects, sort them by age in ascending order, and then by name alphabetically for people with the same age.
Person[] pList1 = {new Person("Alice", 25), new Person("Bob", 30),
    new Person("Charlie", 25)};
Person[] pList2 = {new Person("David", 30), new Person("Eve", 25),
    new Person("Alice", 25)};

Stream.concat(Arrays.stream(pList1), Arrays.stream(pList2))
    .sorted(Comparator.comparingInt(Person::getAge)
        .thenComparing(Person::getName))
    .forEach(System.out::println);
Problem 4: Find the length of the longest name in a list of strings.
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Eva");
int maxLength = names.stream()
    .mapToInt(String::length)
    .max()
    .orElse(0);
Problem 5: Check if a list of integers contains any prime numbers.
List<Integer> numbers = Arrays.asList(4, 6, 8, 11, 12, 13, 14, 15);
boolean hasPrime = numbers.stream()
    .anyMatch(num -> isPrime(num));

private static boolean isPrime(int num) {
    if (num <= 1) return false;
    return IntStream.rangeClosed(2, (int) Math.sqrt(num))
        .noneMatch(i -> num % i == 0);
}
Problem 6: Count the total number of distinct words (case-insensitive) across multiple sentences.
List<String> sentences = Arrays.asList(
    "Java Stream API provides a fluent interface",
    "It supports functional-style operations on streams",
    "In this exercise, you need to count words"
);

long uniqueWords = sentences.stream()
    .map(x -> x.toLowerCase().split(" "))
    .flatMap(Arrays::stream)
    .distinct()
    .count();
Problem 7: Find and concatenate the first two words that have even lengths.
List<String> words = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");
String result = words.stream()
    .filter(x -> x.length() % 2 == 0)
    .limit(2)
    .collect(Collectors.joining());
Problem 8: Given a list of transactions, find the sum of transaction amounts for each day and sort by date.
class Transaction {
    String date;
    long amount;
    // constructors and getters
}

List<Transaction> transactions = Arrays.asList(
    new Transaction("2022-01-01", 100),
    new Transaction("2022-01-01", 200),
    new Transaction("2022-01-02", 300)
);

Map<String, Long> dailyTotals = transactions.stream()
    .collect(Collectors.groupingBy(
        Transaction::getDate,
        TreeMap::new,
        Collectors.summingLong(Transaction::getAmount)
    ));
Problem 9: Merge two arrays of integers, sort them, and filter out any numbers greater than a specified threshold.
int[] array1 = {1, 5, 3, 9, 7};
int[] array2 = {2, 4, 6, 8, 10};
int threshold = 7;

IntStream.concat(Arrays.stream(array1), Arrays.stream(array2))
    .boxed()
    .sorted(Comparator.naturalOrder())
    .filter(x -> x > threshold)
    .forEach(System.out::println);
Problem 10: Transform a list of employee records into a map of department to average salary.
class Employee {
    String department;
    double salary;
    // constructor and getters
}

Map<String, Double> deptAvgSalary = employees.stream()
    .collect(Collectors.groupingBy(
        Employee::getDepartment,
        Collectors.averagingDouble(Employee::getSalary)
    ));
Problem 11: Partition a list of numbers into two groups: prime and non-prime numbers.
List<Integer> numbers = Arrays.asList(2, 3, 4, 5, 6, 7, 8, 9, 10);
Map<Boolean, List<Integer>> partitioned = numbers.stream()
    .collect(Collectors.partitioningBy(num -> isPrime(num)));
Problem 12: Generate Fibonacci sequence up to n terms using streams.
Stream.iterate(new int[]{0, 1}, 
    arr -> new int[]{arr[1], arr[0] + arr[1]})
    .limit(10)
    .map(arr -> arr[0])
    .forEach(System.out::println);
Problem 13: Group strings by their first character and count occurrences.
List<String> words = Arrays.asList("apple", "banana", "bear", "cat", "apple");
Map<Character, Long> frequency = words.stream()
    .collect(Collectors.groupingBy(
        str -> str.charAt(0),
        Collectors.counting()
    ));
// Output: {a=2, b=2, c=1}
Problem 14: Find the intersection of two lists using Java streams.
List<Integer> list3 = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> list4 = Arrays.asList(3, 4, 5, 6, 7);

List<Integer> intersection =
    list3.stream().filter(list4::contains).toList();
System.out.println(intersection);
Problem 15: How to Convert a List of Objects into a Sorted Map While Handling Duplicate Keys in Java?
 List<Employee> employees = Arrays.asList(
            new Employee(101, "Alice"),
            new Employee(102, "Bob"),
            new Employee(101, "Charlie"),
            new Employee(103, "David"),
            new Employee(102, "Eve")
        );

        // Convert to TreeMap with List as value type
        Map<Integer, List<Employee>> employeeMap = employees.stream()
            .collect(Collectors.groupingBy(
                e -> e.id,               // Key extractor
                TreeMap::new,            // Use TreeMap to maintain sorted order
                Collectors.toList()      // Collect values into a list
            ));
Explanation:
	
	=================================================================================


 Java 8 Interview Coding Questions And Answers :
1) Given a list of integers, separate odd and even numbers?

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(71, 18, 42, 21, 67, 32, 95, 14, 56, 87);
		
		Map<Boolean, List<Integer>> oddEvenNumbersMap = 
				listOfIntegers.stream().collect(Collectors.partitioningBy(i -> i % 2 == 0));
		
		Set<Entry<Boolean, List<Integer>>> entrySet = oddEvenNumbersMap.entrySet();
		
		for (Entry<Boolean, List<Integer>> entry : entrySet) 
		{
			System.out.println("--------------");
			
			if (entry.getKey())
			{
				System.out.println("Even Numbers");
			}
			else
			{
				System.out.println("Odd Numbers");
			}
			
			System.out.println("--------------");
			
			List<Integer> list = entry.getValue();
			
			for (int i : list)
			{
				System.out.println(i);
			}
		}
	}
}
Output :

————–
Odd Numbers
————–
71
21
67
95
87
————–
Even Numbers
————–
18
42
32
14
56
2) How do you remove duplicate elements from a list using Java 8 streams?


import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("Java", "Python", "C#", "Java", "Kotlin", "Python");
		
		List<String> uniqueStrngs = listOfStrings.stream().distinct().collect(Collectors.toList());
		
		System.out.println(uniqueStrngs);
	}
}
Output :

[Java, Python, C#, Kotlin]

3) How do you find frequency of each character in a string using Java 8 streams?

import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String inputString = "Java Concept Of The Day";
		
		Map<Character, Long> charCountMap = 
					inputString.chars()
								.mapToObj(c -> (char) c)
								.collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
		
		System.out.println(charCountMap);
	}
}
Output :

{ =4, a=3, c=1, C=1, D=1, e=2, f=1, h=1, J=1, n=1, O=1, o=1, p=1, T=1, t=1, v=1, y=1}

4) How do you find frequency of each element in an array or a list?

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> stationeryList = Arrays.asList("Pen", "Eraser", "Note Book", "Pen", "Pencil", "Stapler", "Note Book", "Pencil");
		
		Map<String, Long> stationeryCountMap = 
				stationeryList.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
		
		System.out.println(stationeryCountMap);
	}
}
Output :

{Pen=2, Stapler=1, Pencil=2, Note Book=2, Eraser=1}

5) How do you sort the given list of decimals in reverse order?

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Double> decimalList = Arrays.asList(12.45, 23.58, 17.13, 42.89, 33.78, 71.85, 56.98, 21.12);
		
		decimalList.stream().sorted(Comparator.reverseOrder()).forEach(System.out::println);
	}
}
Output :


71.85
56.98
42.89
33.78
23.58
21.12
17.13
12.45

6) Given a list of strings, join the strings with ‘[‘ as prefix, ‘]’ as suffix and ‘,’ as delimiter?

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("Facebook", "Twitter", "YouTube", "WhatsApp", "LinkedIn");
		
		String joinedString = listOfStrings.stream().collect(Collectors.joining(", ", "[", "]"));
		
		System.out.println(joinedString);
	}
}
Output :

[Facebook, Twitter, YouTube, WhatsApp, LinkedIn]

7) From the given list of integers, print the numbers which are multiples of 5?

import java.util.Arrays;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(45, 12, 56, 15, 24, 75, 31, 89);
		
		listOfIntegers.stream().filter(i -> i % 5 == 0).forEach(System.out::println);
	}
}
Output :

45
15
75

8) Given a list of integers, find maximum and minimum of those numbers?

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(45, 12, 56, 15, 24, 75, 31, 89);
		
		int max = listOfIntegers.stream().max(Comparator.naturalOrder()).get();
		
		System.out.println("Maximum Element : "+max);
		
		int min = listOfIntegers.stream().min(Comparator.naturalOrder()).get();
		
		System.out.println("Minimum Element : "+min);
	}
}
Output :

Maximum Element : 89
Minimum Element : 12

9) How do you merge two unsorted arrays into single sorted array using Java 8 streams?

import java.util.Arrays;
import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int[] a = new int[] {4, 2, 7, 1};
		
		int[] b = new int[] {8, 3, 9, 5};
		
		int[] c = IntStream.concat(Arrays.stream(a), Arrays.stream(b)).sorted().toArray();
		
		System.out.println(Arrays.toString(c));
	}
}
Output :

[1, 2, 3, 4, 5, 7, 8, 9]

10) How do you merge two unsorted arrays into single sorted array without duplicates?

import java.util.Arrays;
import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int[] a = new int[] {4, 2, 5, 1};
		
		int[] b = new int[] {8, 1, 9, 5};
		
		int[] c = IntStream.concat(Arrays.stream(a), Arrays.stream(b)).sorted().distinct().toArray();
		
		System.out.println(Arrays.toString(c));
	}
}
Output :

[1, 2, 4, 5, 8, 9]

11) How do you get three maximum numbers and three minimum numbers from the given list of integers?

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(45, 12, 56, 15, 24, 75, 31, 89);
		
		//3 minimum Numbers
		
		System.out.println("-----------------");
		
		System.out.println("Minimum 3 Numbers");
		
		System.out.println("-----------------");
		
		listOfIntegers.stream().sorted().limit(3).forEach(System.out::println);
		
		//3 Maximum Numbers
		
		System.out.println("-----------------");
		
		System.out.println("Maximum 3 Numbers");
		
		System.out.println("-----------------");
		
listOfIntegers.stream().sorted(Comparator.reverseOrder()).limit(3).forEach(System.out::println);
	}
}
Output :

—————–
Minimum 3 Numbers
—————–
12
15
24
—————–
Maximum 3 Numbers
—————–
89
75
56
12) Java 8 program to check if two strings are anagrams or not?

import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String s1 = "RaceCar";
		String s2 = "CarRace";
		
		s1 = Stream.of(s1.split("")).map(String::toUpperCase).sorted().collect(Collectors.joining());
		
		s2 = Stream.of(s2.split("")).map(String::toUpperCase).sorted().collect(Collectors.joining());
		
		if (s1.equals(s2)) 
		{
			System.out.println("Two strings are anagrams");
		}
		else
		{
			System.out.println("Two strings are not anagrams");
		}
	}
}
Output :

Two strings are anagrams

13) Find sum of all digits of a number in Java 8?

import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int i = 15623;
		
		Integer sumOfDigits = Stream.of(String.valueOf(i).split("")).collect(Collectors.summingInt(Integer::parseInt));
		
		System.out.println(sumOfDigits);
	}
}
Output :

17

14) Find second largest number in an integer array?

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(45, 12, 56, 15, 24, 75, 31, 89);
		
		Integer secondLargestNumber = listOfIntegers.stream().sorted(Comparator.reverseOrder()).skip(1).findFirst().get();
		
		System.out.println(secondLargestNumber);
	}
}
Output :

75

15) Given a list of strings, sort them according to increasing order of their length?

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("Java", "Python", "C#", "HTML", "Kotlin", "C++", "COBOL", "C");
		
		listOfStrings.stream().sorted(Comparator.comparing(String::length)).forEach(System.out::println);
	}
}
Output :

C
C#
C++
Java
HTML
COBOL
Python
Kotlin

16) Given an integer array, find sum and average of all elements?

import java.util.Arrays;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int[] a = new int[] {45, 12, 56, 15, 24, 75, 31, 89};
		
		int sum = Arrays.stream(a).sum();
		
		System.out.println("Sum = "+sum);
		
		double average = Arrays.stream(a).average().getAsDouble();
		
		System.out.println("Average = "+average);
	}
}
Output :

Sum = 347
Average = 43.375

17) How do you find common elements between two arrays?

import java.util.Arrays;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> list1 = Arrays.asList(71, 21, 34, 89, 56, 28);
		
		List<Integer> list2 = Arrays.asList(12, 56, 17, 21, 94, 34);
		
		list1.stream().filter(list2::contains).forEach(System.out::println);
	}
}
Output :

21
34
56

18) Reverse each word of a string using Java 8 streams?

import java.util.Arrays;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String str = "Java Concept Of The Day";
		
		String reversedStr = Arrays.stream(str.split(" "))
									.map(word -> new StringBuffer(word).reverse())
									.collect(Collectors.joining(" "));
		
		System.out.println(reversedStr);
	}
}
Output :

avaJ tpecnoC fO ehT yaD

19) How do you find sum of first 10 natural numbers?

import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int sum = IntStream.range(1, 11).sum();
		
		System.out.println(sum);
	}
}
Output :

55

20) Reverse an integer array

import java.util.Arrays;
import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		int[] array = new int[] {5, 1, 7, 3, 9, 6};
		
		int[] reversedArray = IntStream.rangeClosed(1, array.length).map(i -> array[array.length - i]).toArray();
		
		System.out.println(Arrays.toString(reversedArray));
	}
}
Output :

[6, 9, 3, 7, 1, 5]

21) Print first 10 even numbers

import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		IntStream.rangeClosed(1, 10).map(i -> i * 2).forEach(System.out::println);
	}
}
Output :

2
4
6
8
10
12
14
16
18
20

22) How do you find the most repeated element in an array?

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("Pen", "Eraser", "Note Book", "Pen", "Pencil", "Pen", "Note Book", "Pencil");
		
		Map<String, Long> elementCountMap = listOfStrings.stream()
														 .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
		
		Entry<String, Long> mostFrequentElement = elementCountMap.entrySet().stream().max(Map.Entry.comparingByValue()).get();
		
		System.out.println("Most Frequent Element : "+mostFrequentElement.getKey());
		
		System.out.println("Count : "+mostFrequentElement.getValue());
	}
}
Output :

Most Frequent Element : Pen
Count : 3

23) Palindrome program using Java 8 streams

import java.util.stream.IntStream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String str = "ROTATOR";
		
		boolean isItPalindrome = IntStream.range(0, str.length()/2).
                noneMatch(i -> str.charAt(i) != str.charAt(str.length() - i -1));
         
        if (isItPalindrome)
        {
            System.out.println(str+" is a palindrome");
        }
        else
        {
            System.out.println(str+" is not a palindrome");
        }
	}
}
Output :

ROTATOR is a palindrome

24) Given a list of strings, find out those strings which start with a number?

import java.util.Arrays;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("One", "2wo", "3hree", "Four", "5ive", "Six");
		
		listOfStrings.stream().filter(str -> Character.isDigit(str.charAt(0))).forEach(System.out::println);
	}
}
Output :

2wo
3hree
5ive

25) How do you extract duplicate elements from an array?

import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<Integer> listOfIntegers = Arrays.asList(111, 222, 333, 111, 555, 333, 777, 222);
		
		Set<Integer> uniqueElements = new HashSet<>();
		
		Set<Integer> duplicateElements = listOfIntegers.stream().filter(i -> ! uniqueElements.add(i)).collect(Collectors.toSet());
		
		System.out.println(duplicateElements);
	}
}
Output :

[333, 222, 111]

26) Print duplicate characters in a string?

import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String inputString = "Java Concept Of The Day".replaceAll("\\s+", "").toLowerCase();
		
		Set<String> uniqueChars = new HashSet<>();
		
		Set<String> duplicateChars = 
				Arrays.stream(inputString.split(""))
						.filter(ch -> ! uniqueChars.add(ch))
						.collect(Collectors.toSet());
		
		System.out.println(duplicateChars);
	}
}
Output :

[a, c, t, e, o]

27) Find first repeated character in a string?

import java.util.Arrays;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String inputString = "Java Concept Of The Day".replaceAll("\\s+", "").toLowerCase();
		
		Map<String, Long> charCountMap = 
							Arrays.stream(inputString.split(""))
									.collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()));
		
		String firstRepeatedChar = charCountMap.entrySet()
												.stream()
												.filter(entry -> entry.getValue() > 1)
												.map(entry -> entry.getKey())
												.findFirst()
												.get();
		
		System.out.println(firstRepeatedChar);
	}
}
Output :

a

28) Find first non-repeated character in a string?

import java.util.Arrays;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		String inputString = "Java Concept Of The Day".replaceAll("\\s+", "").toLowerCase();
		
		Map<String, Long> charCountMap = 
							Arrays.stream(inputString.split(""))
									.collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()));
		
		String firstNonRepeatedChar = charCountMap.entrySet()
												.stream()
												.filter(entry -> entry.getValue() == 1)
												.map(entry -> entry.getKey())
												.findFirst()
												.get();
		
		System.out.println(firstNonRepeatedChar);
	}
}
Output :

j

29) Fibonacci series

import java.util.stream.Stream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		Stream.iterate(new int[] {0, 1}, f -> new int[] {f[1], f[0]+f[1]})
				.limit(10)
				.map(f -> f[0])
				.forEach(i -> System.out.print(i+" "));
	}
}
Output :

0 1 1 2 3 5 8 13 21 34

30) First 10 odd numbers

import java.util.stream.Stream;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		Stream.iterate(new int[] {1, 3}, f -> new int[] {f[1], f[1]+2})
				.limit(10)
				.map(f -> f[0])
				.forEach(i -> System.out.print(i+" "));
	}
}
Output :

1 3 5 7 9 11 13 15 17 19

31) How do you get last element of an array?

import java.util.Arrays;
import java.util.List;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		List<String> listOfStrings = Arrays.asList("One", "Two", "Three", "Four", "Five", "Six");
		
		String lastElement = listOfStrings.stream().skip(listOfStrings.size() - 1).findFirst().get();
		
		System.out.println(lastElement);
	}
}
Output :

Six

32) Find the age of a person in years if the birthday has given?

import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

public class Java8Code 
{
	public static void main(String[] args) 
	{
		LocalDate birthDay = LocalDate.of(1985, 01, 23);
		LocalDate today = LocalDate.now();
		
		System.out.println(ChronoUnit.YEARS.between(birthDay, today));
	}
}
	
	

}
}


}


//======================================================================================================
                       100             100                100               100             100
//=========================================================================================================


Basic Level Questions (1–20)
1. Find the Sum of All Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sum = numbers.stream().mapToInt(Integer::intValue).sum();
System.out.println("Sum: " + sum);
Output:

Sum: 15
2. Find the Product of All Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int product = numbers.stream().reduce(1, (a, b) -> a * b);
System.out.println("Product: " + product);
Output:

Product: 120
3. Find the Average of All Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
double average = numbers.stream().mapToInt(Integer::intValue).average().orElse(0);
System.out.println("Average: " + average);
Output:

Average: 3.0
4. Find the Maximum Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int max = numbers.stream().max(Integer::compare).orElse(0);
System.out.println("Max: " + max);
Output:

Max: 5
5. Find the Minimum Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int min = numbers.stream().min(Integer::compare).orElse(0);
System.out.println("Min: " + min);
Output:

Min: 1
6. Count the Number of Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
long count = numbers.stream().count();
System.out.println("Count: " + count);
Output:

Count: 5
7. Check if a List Contains a Specific Element

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
boolean contains = numbers.stream().anyMatch(n -> n == 3);
System.out.println("Contains 3: " + contains);
Output:

Contains 3: true
8. Filter Out Even Numbers from a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
System.out.println("Even Numbers: " + evenNumbers);
Output:

Even Numbers: [2, 4]
9. Filter Out Odd Numbers from a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
List<Integer> oddNumbers = numbers.stream()
    .filter(n -> n % 2 != 0)
    .collect(Collectors.toList());
System.out.println("Odd Numbers: " + oddNumbers);
Output:

Odd Numbers: [1, 3, 5]
10. Convert a List of Strings to Uppercase

Solution:

List<String> words = List.of("hello", "world");
List<String> uppercaseWords = words.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());
System.out.println("Uppercase Words: " + uppercaseWords);
Output:

Uppercase Words: [HELLO, WORLD]
11. Convert a List of Integers to Their Squares

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
List<Integer> squares = numbers.stream()
    .map(n -> n * n)
    .collect(Collectors.toList());
System.out.println("Squares: " + squares);
Output:

Squares: [1, 4, 9, 16, 25]
12. Find the First Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int first = numbers.stream().findFirst().orElse(0);
System.out.println("First Element: " + first);
Output:

First Element: 1
13. Find the Last Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int last = numbers.stream().reduce((a, b) -> b).orElse(0);
System.out.println("Last Element: " + last);
Output:

Last Element: 5
14. Check if All Elements in a List Satisfy a Condition

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
boolean allEven = numbers.stream().allMatch(n -> n % 2 == 0);
System.out.println("All Even: " + allEven);
Output:

All Even: false
15. Check if Any Element in a List Satisfies a Condition

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
boolean anyEven = numbers.stream().anyMatch(n -> n % 2 == 0);
System.out.println("Any Even: " + anyEven);
Output:

Any Even: true
16. Remove Duplicate Elements from a List

Solution:

List<Integer> numbers = List.of(1, 2, 2, 3, 4, 4, 5);
List<Integer> uniqueNumbers = numbers.stream()
    .distinct()
    .collect(Collectors.toList());
System.out.println("Unique Numbers: " + uniqueNumbers);
Output:

Unique Numbers: [1, 2, 3, 4, 5]
17. Sort a List of Integers in Ascending Order

Solution:

List<Integer> numbers = List.of(5, 3, 1, 4, 2);
List<Integer> sortedNumbers = numbers.stream()
    .sorted()
    .collect(Collectors.toList());
System.out.println("Sorted Numbers: " + sortedNumbers);
Output:

Sorted Numbers: [1, 2, 3, 4, 5]
18. Sort a List of Integers in Descending Order

Solution:

List<Integer> numbers = List.of(5, 3, 1, 4, 2);
List<Integer> sortedNumbers = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());
System.out.println("Sorted Numbers (Descending): " + sortedNumbers);
Output:

Sorted Numbers (Descending): [5, 4, 3, 2, 1]
19. Sort a List of Strings in Alphabetical Order

Solution:

List<String> words = List.of("banana", "apple", "cherry");
List<String> sortedWords = words.stream()
    .sorted()
    .collect(Collectors.toList());
System.out.println("Sorted Words: " + sortedWords);
Output:

Sorted Words: [apple, banana, cherry]
20. Sort a List of Strings by Their Length

Solution:

List<String> words = List.of("apple", "banana", "kiwi");
List<String> sortedWords = words.stream()
    .sorted(Comparator.comparingInt(String::length))
    .collect(Collectors.toList());
System.out.println("Sorted Words by Length: " + sortedWords);
Output:

Sorted Words by Length: [kiwi, apple, banana]
Intermediate Level Questions (21–40)
21. Find the Sum of Digits of a Number

Solution:

int number = 12345;
int sum = String.valueOf(number).chars()
    .map(Character::getNumericValue)
    .sum();
System.out.println("Sum of Digits: " + sum);
Output:

Sum of Digits: 15
22. Find the Factorial of a Number

Solution:

int number = 5;
int factorial = IntStream.rangeClosed(1, number)
    .reduce(1, (a, b) -> a * b);
System.out.println("Factorial: " + factorial);
Output:

Factorial: 120
23. Find the Second-Largest Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int secondLargest = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .skip(1)
    .findFirst()
    .orElse(0);
System.out.println("Second Largest: " + secondLargest);
Output:

Second Largest: 4
24. Find the Second-Smallest Element in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int secondSmallest = numbers.stream()
    .sorted()
    .skip(1)
    .findFirst()
    .orElse(0);
System.out.println("Second Smallest: " + secondSmallest);
Output:

Second Smallest: 2
25. Find the Longest String in a List

Solution:

List<String> words = List.of("apple", "banana", "kiwi");
String longest = words.stream()
    .max(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Longest Word: " + longest);
Output:

Longest Word: banana
26. Find the Shortest String in a List

Solution:

List<String> words = List.of("apple", "banana", "kiwi");
String shortest = words.stream()
    .min(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Shortest Word: " + shortest);
Output:

Shortest Word: kiwi
27. Group a List of Strings by Their Length

Solution:

List<String> words = List.of("apple", "banana", "kiwi");
Map<Integer, List<String>> groupedByLength = words.stream()
    .collect(Collectors.groupingBy(String::length));
System.out.println("Grouped by Length: " + groupedByLength);
Output:

Grouped by Length: {4=[kiwi], 5=[apple], 6=[banana]}
28. Group a List of Objects by a Specific Attribute

Solution:

class Person {
    String name;
    int age;
    // Constructor, getters, and setters
}

List<Person> people = List.of(
    new Person("Alice", 25),
    new Person("Bob", 30),
    new Person("Charlie", 25)
);

Map<Integer, List<Person>> groupedByAge = people.stream()
    .collect(Collectors.groupingBy(Person::getAge));
System.out.println("Grouped by Age: " + groupedByAge);
Output:

Grouped by Age: {25=[Alice, Charlie], 30=[Bob]}
29. Partition a List of Integers into Even and Odd Numbers

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
Map<Boolean, List<Integer>> partitioned = numbers.stream()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));
System.out.println("Partitioned: " + partitioned);
Output:

Partitioned: {false=[1, 3, 5], true=[2, 4]}
30. Merge Two Lists into a Single List

Solution:

List<Integer> list1 = List.of(1, 2, 3);
List<Integer> list2 = List.of(4, 5, 6);
List<Integer> merged = Stream.concat(list1.stream(), list2.stream())
    .collect(Collectors.toList());
System.out.println("Merged List: " + merged);
Output:

Merged List: [1, 2, 3, 4, 5, 6]
31. Find the Intersection of Two Lists

Solution:

List<Integer> list1 = List.of(1, 2, 3, 4);
List<Integer> list2 = List.of(3, 4, 5, 6);
List<Integer> intersection = list1.stream()
    .filter(list2::contains)
    .collect(Collectors.toList());
System.out.println("Intersection: " + intersection);
Output:

Intersection: [3, 4]
32. Find the Union of Two Lists

Solution:

List<Integer> list1 = List.of(1, 2, 3);
List<Integer> list2 = List.of(3, 4, 5);
List<Integer> union = Stream.concat(list1.stream(), list2.stream())
    .distinct()
    .collect(Collectors.toList());
System.out.println("Union: " + union);
Output:

Union: [1, 2, 3, 4, 5]
33. Find the Difference Between Two Lists

Solution:

List<Integer> list1 = List.of(1, 2, 3, 4);
List<Integer> list2 = List.of(3, 4, 5, 6);
List<Integer> difference = list1.stream()
    .filter(n -> !list2.contains(n))
    .collect(Collectors.toList());
System.out.println("Difference: " + difference);
Output:

Difference: [1, 2]
34. Count the Occurrences of Each Element in a List

Solution:

List<String> words = List.of("apple", "banana", "apple", "orange");
Map<String, Long> wordCounts = words.stream()
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()));
System.out.println("Word Counts: " + wordCounts);
Output:

Word Counts: {orange=1, banana=1, apple=2}
35. Count the Occurrences of Each Character in a String

Solution:

String input = "hello";
Map<Character, Long> charCounts = input.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
System.out.println("Character Counts: " + charCounts);
Output:

Character Counts: {e=1, h=1, l=2, o=1}
36. Count the Occurrences of Each Word in a String

Solution:

String input = "hello world hello";
Map<String, Long> wordCounts = Arrays.stream(input.split(" "))
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()));
System.out.println("Word Counts: " + wordCounts);
Output:

Word Counts: {hello=2, world=1}
37. Count the Occurrences of Each Vowel in a String

Solution:

String input = "hello world";
Map<Character, Long> vowelCounts = input.chars()
    .mapToObj(c -> (char) c)
    .filter(c -> "aeiou".contains(String.valueOf(c)))
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
System.out.println("Vowel Counts: " + vowelCounts);
Output:

Vowel Counts: {e=1, o=2}
38. Count the Occurrences of Each Digit in a String

Solution:

String input = "hello 123 world 456";
Map<Character, Long> digitCounts = input.chars()
    .mapToObj(c -> (char) c)
    .filter(Character::isDigit)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
System.out.println("Digit Counts: " + digitCounts);
Output:

Digit Counts: {1=1, 2=1, 3=1, 4=1, 5=1, 6=1}
39. Reverse a List Using Streams

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
List<Integer> reversed = numbers.stream()
    .collect(Collectors.collectingAndThen(Collectors.toList(), list -> {
        Collections.reverse(list);
        return list;
    }));
System.out.println("Reversed List: " + reversed);
Output:

Reversed List: [5, 4, 3, 2, 1]
40. Reverse a String Using Streams

Solution:

String input = "hello";
String reversed = input.chars()
    .mapToObj(c -> String.valueOf((char) c))
    .reduce("", (a, b) -> b + a);
System.out.println("Reversed String: " + reversed);
Output:

Reversed String: olleh
Advanced Level Questions (41–60)
41. Find the Most Frequent Element in a List

Solution:

List<String> words = List.of("apple", "banana", "apple", "orange", "banana", "apple");
String mostFrequent = words.stream()
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()))
    .entrySet().stream()
    .max(Map.Entry.comparingByValue())
    .map(Map.Entry::getKey)
    .orElse(null);
System.out.println("Most Frequent: " + mostFrequent);
Output:

Most Frequent: apple
42. Find the Least Frequent Element in a List

Solution:

List<String> words = List.of("apple", "banana", "apple", "orange", "banana", "apple");
String leastFrequent = words.stream()
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()))
    .entrySet().stream()
    .min(Map.Entry.comparingByValue())
    .map(Map.Entry::getKey)
    .orElse(null);
System.out.println("Least Frequent: " + leastFrequent);
Output:

Least Frequent: orange
43. Find the First Non-Repeated Character in a String

Solution:

String input = "hello";
Character firstNonRepeated = input.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(entry -> entry.getValue() == 1)
    .map(Map.Entry::getKey)
    .findFirst()
    .orElse(null);
System.out.println("First Non-Repeated Character: " + firstNonRepeated);
Output:

First Non-Repeated Character: h
44. Find the First Repeated Character in a String

Solution:

String input = "hello";
Character firstRepeated = input.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(entry -> entry.getValue() > 1)
    .map(Map.Entry::getKey)
    .findFirst()
    .orElse(null);
System.out.println("First Repeated Character: " + firstRepeated);
Output:

First Repeated Character: l
45. Check if a String is a Palindrome

Solution:

String input = "madam";
boolean isPalindrome = IntStream.range(0, input.length() / 2)
    .allMatch(i -> input.charAt(i) == input.charAt(input.length() - 1 - i));
System.out.println("Is Palindrome: " + isPalindrome);
Output:

Is Palindrome: true
46. Find All Anagrams of a String from a List

Solution:

List<String> words = List.of("listen", "silent", "enlist", "google", "inlets");
String target = "silent";
List<String> anagrams = words.stream()
    .filter(word -> Arrays.equals(
        word.chars().sorted().toArray(),
        target.chars().sorted().toArray()
    ))
    .collect(Collectors.toList());
System.out.println("Anagrams: " + anagrams);
Output:

Anagrams: [silent, inlets]
47. Generate the Fibonacci Sequence Using Streams

Solution:

Stream.iterate(new int[]{0, 1}, fib -> new int[]{fib[1], fib[0] + fib[1]})
    .limit(10)
    .map(fib -> fib[0])
    .forEach(System.out::println);
Output:

0
1
1
2
3
5
8
13
21
34
48. Generate a List of Random Numbers Using Streams

Solution:

List<Integer> randomNumbers = Stream.generate(() -> new Random().nextInt(100))
    .limit(10)
    .collect(Collectors.toList());
System.out.println("Random Numbers: " + randomNumbers);
Output:

Random Numbers: [42, 67, 23, 89, 12, 45, 78, 34, 56, 90]
49. Flatten a List of Lists into a Single List

Solution:

List<List<Integer>> listOfLists = List.of(
    List.of(1, 2, 3),
    List.of(4, 5, 6),
    List.of(7, 8, 9)
);
List<Integer> flattened = listOfLists.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());
System.out.println("Flattened List: " + flattened);
Output:

Flattened List: [1, 2, 3, 4, 5, 6, 7, 8, 9]
50. Find the Sum of All Even Numbers in a Nested List

Solution:

List<List<Integer>> listOfLists = List.of(
    List.of(1, 2, 3),
    List.of(4, 5, 6),
    List.of(7, 8, 9)
);
int sum = listOfLists.stream()
    .flatMap(List::stream)
    .filter(n -> n % 2 == 0)
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum of Even Numbers: " + sum);
Output:

Sum of Even Numbers: 20
51. Find the Sum of All Odd Numbers in a Nested List

Solution:

List<List<Integer>> listOfLists = List.of(
    List.of(1, 2, 3),
    List.of(4, 5, 6),
    List.of(7, 8, 9)
);
int sum = listOfLists.stream()
    .flatMap(List::stream)
    .filter(n -> n % 2 != 0)
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum of Odd Numbers: " + sum);
Output:

Sum of Odd Numbers: 25
52. Find the Longest Palindrome in a List of Strings

Solution:

List<String> words = List.of("madam", "racecar", "apple", "banana", "level");
String longestPalindrome = words.stream()
    .filter(word -> word.equals(new StringBuilder(word).reverse().toString()))
    .max(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Longest Palindrome: " + longestPalindrome);
Output:

Longest Palindrome: racecar
53. Find the Shortest Palindrome in a List of Strings

Solution:

List<String> words = List.of("madam", "racecar", "apple", "banana", "level");
String shortestPalindrome = words.stream()
    .filter(word -> word.equals(new StringBuilder(word).reverse().toString()))
    .min(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Shortest Palindrome: " + shortestPalindrome);
Output:

Shortest Palindrome: level
54. Find the Longest Word in a String

Solution:

String input = "hello world this is a test";
String longestWord = Arrays.stream(input.split(" "))
    .max(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Longest Word: " + longestWord);
Output:

Longest Word: hello
55. Find the Shortest Word in a String

Solution:

String input = "hello world this is a test";
String shortestWord = Arrays.stream(input.split(" "))
    .min(Comparator.comparingInt(String::length))
    .orElse("");
System.out.println("Shortest Word: " + shortestWord);
Output:

Shortest Word: a
56. Find the Number of Words in a String

Solution:

String input = "hello world this is a test";
long wordCount = Arrays.stream(input.split(" ")).count();
System.out.println("Word Count: " + wordCount);
Output:

Word Count: 6
57. Find the Number of Lines in a File

Solution:

Path path = Paths.get("sample.txt");
long lineCount = Files.lines(path).count();
System.out.println("Line Count: " + lineCount);
Output:

Line Count: 10
58. Find the Number of Characters in a File

Solution:

Path path = Paths.get("sample.txt");
long charCount = Files.lines(path)
    .flatMapToInt(String::chars)
    .count();
System.out.println("Character Count: " + charCount);
Output:

Character Count: 100
59. Find the Number of Words in a File

Solution:

Path path = Paths.get("sample.txt");
long wordCount = Files.lines(path)
    .flatMap(line -> Arrays.stream(line.split(" ")))
    .count();
System.out.println("Word Count: " + wordCount);
Output:

Word Count: 50
60. Find the Number of Unique Words in a File

Solution:

Path path = Paths.get("sample.txt");
long uniqueWordCount = Files.lines(path)
    .flatMap(line -> Arrays.stream(line.split(" ")))
    .distinct()
    .count();
System.out.println("Unique Word Count: " + uniqueWordCount);
Output:

Unique Word Count: 30
Real-World Use Case Questions (61–70)
61. Process a CSV File and Calculate Aggregate Statistics

Solution:

Path path = Paths.get("data.csv");
Map<String, Double> averageSalaryByDept = Files.lines(path)
    .skip(1) // Skip header
    .map(line -> line.split(","))
    .collect(Collectors.groupingBy(
        fields -> fields[1], // Department
        Collectors.averagingDouble(fields -> Double.parseDouble(fields[2])) // Salary
    ));
System.out.println("Average Salary by Department: " + averageSalaryByDept);
Output:

Average Salary by Department: {HR=50000.0, IT=60000.0, Sales=45000.0}
62. Filter and Transform Data Fetched from a Database

Solution:

List<Employee> employees = // Fetch from database
Map<String, List<String>> namesByDept = employees.stream()
    .filter(e -> e.getSalary() > 50000)
    .collect(Collectors.groupingBy(
        Employee::getDepartment,
        Collectors.mapping(Employee::getName, Collectors.toList())
    ));
System.out.println("Names by Department: " + namesByDept);
Output:

Names by Department: {HR=[Alice], IT=[Bob, Charlie]}
63. Parse and Validate JSON Payloads

Solution:

String json = "[{\"name\":\"Alice\",\"age\":25},{\"name\":\"Bob\",\"age\":30}]";
List<Person> people = new ObjectMapper().readValue(json, new TypeReference<List<Person>>() {});
List<String> validNames = people.stream()
    .filter(p -> p.getAge() > 25)
    .map(Person::getName)
    .collect(Collectors.toList());
System.out.println("Valid Names: " + validNames);
Output:

Valid Names: [Bob]
64. Combine Multiple Asynchronous Tasks

Solution:

CompletableFuture<List<Integer>> future1 = CompletableFuture.supplyAsync(() -> List.of(1, 2, 3));
CompletableFuture<List<Integer>> future2 = CompletableFuture.supplyAsync(() -> List.of(4, 5, 6));
List<Integer> combined = Stream.of(future1, future2)
    .map(CompletableFuture::join)
    .flatMap(List::stream)
    .collect(Collectors.toList());
System.out.println("Combined List: " + combined);
Output:

Combined List: [1, 2, 3, 4, 5, 6]
65. Process Large Datasets in Parallel

Solution:

List<Integer> numbers = IntStream.rangeClosed(1, 1000000).boxed().collect(Collectors.toList());
long sum = numbers.parallelStream()
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum: " + sum);
Output:

Sum: 500000500000
66. Handle Exceptions in Streams

Solution:

List<String> numbers = List.of("1", "2", "three", "4");
List<Integer> parsedNumbers = numbers.stream()
    .flatMap(s -> {
        try {
            return Stream.of(Integer.parseInt(s));
        } catch (NumberFormatException e) {
            return Stream.empty();
        }
    })
    .collect(Collectors.toList());
System.out.println("Parsed Numbers: " + parsedNumbers);
Output:

Parsed Numbers: [1, 2, 4]
67. Use Custom Collectors to Calculate Statistics

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
DoubleSummaryStatistics stats = numbers.stream()
    .collect(Collectors.summarizingDouble(Integer::intValue));
System.out.println("Stats: " + stats);
Output:

Stats: DoubleSummaryStatistics{count=5, sum=15.000000, min=1.000000, average=3.000000, max=5.000000}
68. Group Employees by Department and Calculate Average Salary

Solution:

List<Employee> employees = List.of(
    new Employee("Alice", "HR", 50000),
    new Employee("Bob", "IT", 60000),
    new Employee("Charlie", "HR", 55000)
);
Map<String, Double> avgSalaryByDept = employees.stream()
    .collect(Collectors.groupingBy(
        Employee::getDepartment,
        Collectors.averagingDouble(Employee::getSalary)
    ));
System.out.println("Average Salary by Department: " + avgSalaryByDept);
Output:

Average Salary by Department: {HR=52500.0, IT=60000.0}
67. Find the Top N Highest-Paid Employees

Solution:

List<Employee> employees = List.of(
    new Employee("Alice", "HR", 50000),
    new Employee("Bob", "IT", 60000),
    new Employee("Charlie", "HR", 55000)
);
List<Employee> topN = employees.stream()
    .sorted(Comparator.comparingDouble(Employee::getSalary).reversed())
    .limit(2)
    .collect(Collectors.toList());
System.out.println("Top 2 Employees: " + topN);
Output:

Top 2 Employees: [Bob, Charlie]
70. Find the Top N Most Frequent Words in a Text File

Solution:

Path path = Paths.get("sample.txt");
List<String> topNWords = Files.lines(path)
    .flatMap(line -> Arrays.stream(line.split(" ")))
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()))
    .entrySet().stream()
    .sorted(Map.Entry.<String, Long>comparingByValue().reversed())
    .limit(3)
    .map(Map.Entry::getKey)
    .collect(Collectors.toList());
System.out.println("Top 3 Words: " + topNWords);
Output:

Top 3 Words: [the, and, of]
String Manipulation Questions (71–80)
71. Remove All Vowels from a String

Solution:

String input = "hello world";
String result = input.chars()
    .filter(c -> !"aeiou".contains(String.valueOf((char) c)))
    .mapToObj(c -> String.valueOf((char) c))
    .collect(Collectors.joining());
System.out.println("Result: " + result);
Output:

Result: hll wrld
72. Remove All Consonants from a String

Solution:

String input = "hello world";
String result = input.chars()
    .filter(c -> "aeiou".contains(String.valueOf((char) c)))
    .mapToObj(c -> String.valueOf((char) c))
    .collect(Collectors.joining());
System.out.println("Result: " + result);
Output:

Result: eoo
73. Remove All Digits from a String

Solution:

String input = "hello 123 world";
String result = input.chars()
    .filter(c -> !Character.isDigit(c))
    .mapToObj(c -> String.valueOf((char) c))
    .collect(Collectors.joining());
System.out.println("Result: " + result);
Output:

Result: hello  world
74. Remove All Special Characters from a String

Solution:

String input = "hello@world!";
String result = input.chars()
    .filter(c -> Character.isLetterOrDigit(c) || Character.isWhitespace(c))
    .mapToObj(c -> String.valueOf((char) c))
    .collect(Collectors.joining());
System.out.println("Result: " + result);
Output:

Result: hello world
75. Extract All Digits from a String and Sum Them

Solution:

String input = "hello 123 world 456";
int sum = input.chars()
    .filter(Character::isDigit)
    .map(Character::getNumericValue)
    .sum();
System.out.println("Sum of Digits: " + sum);
Output:

Sum of Digits: 21
76. Extract All Words from a String and Count Their Occurrences

Solution:

String input = "hello world hello";
Map<String, Long> wordCounts = Arrays.stream(input.split(" "))
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()));
System.out.println("Word Counts: " + wordCounts);Output:
Word Counts: {hello=2, world=1}
77. Extract All Unique Words from a String

Solution:

String input = "hello world hello";
List<String> uniqueWords = Arrays.stream(input.split(" "))
    .distinct()
    .collect(Collectors.toList());
System.out.println("Unique Words: " + uniqueWords);Output:
Unique Words: [hello, world]
78. Extract All Palindromic Words from a String

Solution:

String input = "madam racecar apple banana level";
List<String> palindromes = Arrays.stream(input.split(" "))
    .filter(word -> word.equals(new StringBuilder(word).reverse().toString()))
    .collect(Collectors.toList());
System.out.println("Palindromes: " + palindromes);
Output:

Palindromes: [madam, racecar, level]
79. Extract All Words Starting with a Specific Letter

Solution:

String input = "hello world this is a test";
List<String> wordsStartingWithT = Arrays.stream(input.split(" "))
    .filter(word -> word.startsWith("t"))
    .collect(Collectors.toList());
System.out.println("Words Starting with 't': " + wordsStartingWithT);
Output:

Words Starting with 't': [this, test]
80. Extract All Words Ending with a Specific Letter

Solution:

String input = "hello world this is a test";
List<String> wordsEndingWithD = Arrays.stream(input.split(" "))
    .filter(word -> word.endsWith("d"))
    .collect(Collectors.toList());
System.out.println("Words Ending with 'd': " + wordsEndingWithD);
Output:

Words Ending with 'd': [world]
Mathematical and Statistical Questions (81–90)
81. Find the Standard Deviation of a List of Numbers

Solution:

List<Double> numbers = List.of(1.0, 2.0, 3.0, 4.0, 5.0);
double mean = numbers.stream().mapToDouble(Double::doubleValue).average().orElse(0);
double variance = numbers.stream()
    .mapToDouble(n -> Math.pow(n - mean, 2))
    .average().orElse(0);
double stdDev = Math.sqrt(variance);
System.out.println("Standard Deviation: " + stdDev);
Output:

Standard Deviation: 1.4142135623730951
82. Find the Median of a List of Numbers

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
double median = numbers.stream()
    .sorted()
    .skip((numbers.size() - 1) / 2)
    .limit(2 - numbers.size() % 2)
    .mapToInt(Integer::intValue)
    .average()
    .orElse(0);
System.out.println("Median: " + median);
Output:

Median: 3.0
83. Find the Mode of a List of Numbers

Solution:

List<Integer> numbers = List.of(1, 2, 2, 3, 4, 4, 4);
Map<Integer, Long> frequencyMap = numbers.stream()
    .collect(Collectors.groupingBy(n -> n, Collectors.counting()));
int mode = frequencyMap.entrySet().stream()
    .max(Map.Entry.comparingByValue())
    .map(Map.Entry::getKey)
    .orElse(0);
System.out.println("Mode: " + mode);
Output:

Mode: 4
84. Find the Sum of Squares of All Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sumOfSquares = numbers.stream()
    .mapToInt(n -> n * n)
    .sum();
System.out.println("Sum of Squares: " + sumOfSquares);
Output:

Sum of Squares: 55
85. Find the Sum of Cubes of All Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sumOfCubes = numbers.stream()
    .mapToInt(n -> n * n * n)
    .sum();
System.out.println("Sum of Cubes: " + sumOfCubes);
Output:

Sum of Cubes: 225
86. Find the Sum of All Prime Numbers in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int sumOfPrimes = numbers.stream()
    .filter(n -> n > 1 && IntStream.rangeClosed(2, (int) Math.sqrt(n)).noneMatch(i -> n % i == 0))
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum of Primes: " + sumOfPrimes);
Output:

Sum of Primes: 17
87. Find the Sum of All Fibonacci Numbers in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int sumOfFibonacci = numbers.stream()
    .filter(n -> {
        int a = 0, b = 1;
        while (b < n) {
            int temp = b;
            b = a + b;
            a = temp;
        }
        return b == n;
    })
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum of Fibonacci Numbers: " + sumOfFibonacci);
Output:

Sum of Fibonacci Numbers: 20
88. Find the Sum of All Even-Indexed Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int sumOfEvenIndexed = IntStream.range(0, numbers.size())
    .filter(i -> i % 2 == 0)
    .map(numbers::get)
    .sum();
System.out.println("Sum of Even-Indexed Elements: " + sumOfEvenIndexed);
Output:

Sum of Even-Indexed Elements: 25
89. Find the Sum of All Odd-Indexed Elements in a List

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int sumOfOddIndexed = IntStream.range(0, numbers.size())
    .filter(i -> i % 2 != 0)
    .map(numbers::get)
    .sum();
System.out.println("Sum of Odd-Indexed Elements: " + sumOfOddIndexed);
Output:

Sum of Odd-Indexed Elements: 30
90. Find the Sum of All Elements Greater Than a Specific Value

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int threshold = 5;
int sum = numbers.stream()
    .filter(n -> n > threshold)
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum of Elements > " + threshold + ": " + sum);
Output:

Sum of Elements > 5: 40
Parallel Streams Questions (91–100)
91. Process a Large List of Numbers in Parallel

Solution:

List<Integer> numbers = IntStream.rangeClosed(1, 1000000).boxed().collect(Collectors.toList());
long sum = numbers.parallelStream()
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum: " + sum);
Output:

Sum: 500000500000
92. Find the Sum of All Elements in a List Using Parallel Streams

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sum = numbers.parallelStream()
    .mapToInt(Integer::intValue)
    .sum();
System.out.println("Sum: " + sum);
Output:

Sum: 15
93. Find the Maximum Element in a List Using Parallel Streams

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int max = numbers.parallelStream()
    .max(Integer::compare)
    .orElse(0);
System.out.println("Max: " + max);
Output:

Max: 5
94. Find the Minimum Element in a List Using Parallel Streams

Solution:

List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int min = numbers.parallelStream()
    .min(Integer::compare)
    .orElse(0);
System.out.println("Min: " + min);
Output:

Min: 1
95. Sort a List of Integers in Parallel Using Parallel Streams

Solution:

List<Integer> numbers = List.of(5, 3, 1, 4, 2);
List<Integer> sortedNumbers = numbers.parallelStream()
    .sorted()
    .collect(Collectors.toList());
System.out.println("Sorted Numbers: " + sortedNumbers);
Output:

Sorted Numbers: [1, 2, 3, 4, 5]96. Find the Product of All Elements in a List
96. Filter a List of Strings in Parallel Using Parallel Streams

Solution:

List<String> words = List.of("apple", "banana", "kiwi", "mango");
List<String> filteredWords = words.parallelStream()
    .filter(word -> word.length() > 4)
    .collect(Collectors.toList());
System.out.println("Filtered Words: " + filteredWords);
Output:

Filtered Words: [apple, banana, mango]
97. Count the Occurrences of Each Element in a List Using Parallel Streams

Solution:

List<String> words = List.of("apple", "banana", "apple", "orange");
Map<String, Long> wordCounts = words.parallelStream()
    .collect(Collectors.groupingByConcurrent(s -> s, Collectors.counting()));
System.out.println("Word Counts: " + wordCounts);
Output:

Word Counts: {orange=1, banana=1, apple=2}
98. Group a List of Objects by a Specific Attribute Using Parallel Streams

Solution:

class Employee {
    String name;
    String department;
    // Constructor, getters, and setters
}

List<Employee> employees = List.of(
    new Employee("Alice", "HR"),
    new Employee("Bob", "IT"),
    new Employee("Charlie", "HR")
);

Map<String, List<Employee>> groupedByDept = employees.parallelStream()
    .collect(Collectors.groupingByConcurrent(Employee::getDepartment));
System.out.println("Grouped by Department: " + groupedByDept);
Output:

Grouped by Department: {HR=[Alice, Charlie], IT=[Bob]}
99. Merge Two Lists in Parallel Using Parallel Streams

Solution:

List<Integer> list1 = List.of(1, 2, 3);
List<Integer> list2 = List.of(4, 5, 6);
List<Integer> merged = Stream.concat(list1.parallelStream(), list2.parallelStream())
    .collect(Collectors.toList());
System.out.println("Merged List: " + merged);Output:
Merged List: [1, 2, 3, 4, 5, 6]
100. Find the Intersection of Two Lists Using Parallel Streams

Solution:

List<I
