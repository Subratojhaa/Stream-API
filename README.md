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
