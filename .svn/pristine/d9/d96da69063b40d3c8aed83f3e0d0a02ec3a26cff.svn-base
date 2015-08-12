/*
 * TCSS 342 Winter 2013
 * Assignment 4
 */

import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.InputMismatchException;
import java.util.List;
import java.util.Locale;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.Set;
import java.util.TreeMap;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Program to count words within a given text.
 * 
 * @author Raymond Luu
 * @version Winter 2013
 * 
 */
public final class WordCount
{
  
  /**
   * Constant String for TreeMap "t".
   */
  private static final String T_STRING = "t";
  
  /**
   * Constant String for HashMap "h".
   */
  private static final String H_STRING = "h";
  
  /**
   * Nanoseconds (ns) string.
   */
  private static final String NANOSECONDS = " ns";
  
  /**
   * The designated file.
   */
  private static File my_file;
  
  /**
   * File found boolean.
   */
  private static boolean my_file_found;
  
  /**
   * String input to decide to use Hash or Tree Map.
   */
  private static String my_str_input;
  
  /**
   * My list of inputs from file.
   */
  private static List<String> my_list = new ArrayList<String>();
  
  /**
   * TreeMap of the list.
   */
  private static Map<String, Integer> my_tree_map = new TreeMap<String, Integer>();
  
  /**
   * HashMap of the list.
   */
  private static Map<String, Integer> my_hash_map = new HashMap<String, Integer>();
  
  /**
   * Top 10 list.
   */
  private static List<String> my_top_ten_list = new ArrayList<String>();
  
  /**
   * Top 10 list occurrences.
   */
  private static List<Integer> my_top_ten_occurrence_list = new ArrayList<Integer>();
  
  /**
   * Private constructor for this program.
   */
  private WordCount()
  {
    super();
  }
  
  /**
   * Ask user for file name.
   */
  public static void userInput()
  {
    final Scanner user_input = new Scanner(System.in);
    System.out.println("Enter a file name to get started: ");
    final String file_name = user_input.nextLine();
    my_file = new File(file_name);
    
    if (my_file_found)
    {
      user_input.close();
    }
  }
  
  /**
   * Scans input from given file.
   */
  public static void scanInput()
  {
    Scanner input_file;
    try
    {
      input_file = new Scanner(my_file);
      
      while (input_file.hasNext())
      {
        my_list.add(input_file.next());
      }
      
      my_file_found = true;
      input_file.close();
    }
    catch (final FileNotFoundException e)
    {
      System.out.println("File doesn't exist, try again.");
      my_file_found = false;
    }
  }
  
  /**
   * Regular Expression method.
   * 
   * @param the_regex the regular expression.
   * @param the_str the string to check.
   */
  public static void regexChecker(final String the_regex, final String the_str)
  {
    
    String match_found = "";
    
    final Pattern check_regex = Pattern.compile(the_regex);
    
    final Matcher regex_matcher = check_regex.matcher(the_str);
    
    while (regex_matcher.find())
    {
      if (regex_matcher.group().length() != 0)
      {
        match_found = regex_matcher.group().trim();
        match_found = match_found.toLowerCase(Locale.getDefault());
      }
      
      
      // Add match found into tree map.
      if (T_STRING.equals(my_str_input))
      {
        addToTreeMap(match_found);
      }
      
      // Add match found into hash map.
      if (H_STRING.equals(my_str_input))
      {
        addToHashMap(match_found);
      }
      
    }
  }
  
  /**
   * Add regular expression matched words into treeMap.
   * 
   * @param the_str the string.
   */
  public static void addToTreeMap(final String the_str)
  {
    if (my_tree_map.containsKey(the_str))
    {
      my_tree_map.put(the_str, my_tree_map.get(the_str) + 1);
    }
    else
    {
      my_tree_map.put(the_str, 1);
    }
  }
  
  /**
   * Add regular expression matched words into hashMap.
   * 
   * @param the_str the string.
   */
  public static void addToHashMap(final String the_str)
  {
    if (my_hash_map.containsKey(the_str))
    {
      my_hash_map.put(the_str, my_hash_map.get(the_str) + 1);
    }
    else
    {
      my_hash_map.put(the_str, 1);
    }
  }
  
  /**
   * Select top N list.
   * 
   * @return selected number for top N list size.
   */
  public static int selectNList()
  {
    final Scanner user_input = new Scanner(System.in);
    System.out.println("Enter a number for Top N list you would like to see: ");
    int selected_number = -1;
    try
    {
      selected_number = user_input.nextInt();
    }
    catch (final InputMismatchException e)
    {
      System.out.println("Invalid input. Try again.");
    }
    user_input.close();
    return selected_number;
  }
  
  /**
   * Create top N list.
   * 
   * @param the_top_list_size user input top list size.
   */
  public static void createTopList(final int the_top_list_size)
  {
    // Top N words
    
    for (int i = 0; i < the_top_list_size; i++)
    {
      int largest = 0;
      
      Set<Entry<String, Integer>> temp_set = new HashSet<Entry<String, Integer>>();
      
      if (T_STRING.equals(my_str_input))
      {
        temp_set = my_tree_map.entrySet();
      }
      if (H_STRING.equals(my_str_input))
      {
        temp_set = my_hash_map.entrySet();
      }
      
      
      for (Map.Entry<String, Integer> temp_map :  temp_set)
      {
        if (temp_map.getValue() > largest)
        {
          largest = temp_map.getValue();
        }
      }
      
      Map.Entry<String, Integer> remove_map = null;
      for (Map.Entry<String, Integer> temp_map : temp_set)
      {
        if (temp_map.getValue() == largest)
        {
          my_top_ten_list.add(temp_map.getKey());
          my_top_ten_occurrence_list.add(temp_map.getValue());
          remove_map = temp_map;
        }
      }
      temp_set.remove(remove_map);
    }
  }
  
  /**
   * Run program.
   */
  public static void runProgram()
  {
    while (!my_file_found)
    {
      userInput();
      scanInput();
    }
    
    final Scanner user_input = new Scanner(System.in);
    
    while (!T_STRING.equals(my_str_input) && !H_STRING.equals(my_str_input))
    {
      System.out.println("Would you like to use Hash or Tree Map? (h or t): ");
      my_str_input = user_input.nextLine();
      if (!T_STRING.equals(my_str_input) && !H_STRING.equals(my_str_input))
      {
        System.out.println("Invalid input, Try again.");
      }
    }
    
    // time tests before
    Long time1 = System.nanoTime();
    System.out.println("Time before adding full text to Map: " + time1 + NANOSECONDS);
    
    for (int i = 0; i < my_list.size(); i++)
    {
      regexChecker("[A-Za-z]{1,20}", my_list.get(i));
    }
    
    // time tests after
    Long time2 = System.nanoTime();
    System.out.println("Time after adding full text to Map: " + time2 + NANOSECONDS);
    System.out.println("Time it took to add full text to Map: " + (time2 - time1) 
                       + NANOSECONDS);
    System.out.println();
    
    final int top_list_size = selectNList();
    
    // time tests before
    time1 = System.nanoTime();
    System.out.println("Time before adding top N to List: " + time1 + NANOSECONDS);
    
    createTopList(top_list_size);
    
    // time tests after
    time2 = System.nanoTime();
    System.out.println("Time after adding top N to List: " + time2 + NANOSECONDS);
    System.out.println("Time it took to add to Map: " + (time2 - time1) + NANOSECONDS);
    System.out.println();
    
    for (int i = 0; i < my_top_ten_list.size(); i++)
    {
      System.out.println((i + 1) + ". " + my_top_ten_list.get(i) + " - "
                          + my_top_ten_occurrence_list.get(i));
    }
    
    user_input.close();
  }
  
  /**
   * Main method.
   * 
   * @param the_args the argument. 
   */
  public static void main(final String[] the_args)
  { 
    System.out.println("Welcome to WordCount!");
    System.out.println();
    runProgram();
  }
}
