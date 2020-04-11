package flashcards;
import java.io.*;
import java.util.*;

public class Main {
    static String importFile = "./";
    static String exportFile = "./";
    private static Object getKeyFromValue(Map hm, Object value) {
        for (Object o : hm.keySet()) {
            if (hm.get(o).equals(value)) {
                return o;
            }
        }
        return null;
    }

    private static List<Object> getKeyFromValue2(Map hm, Object value) {
        List<Object> rtn = new ArrayList<>();
        for (Object o : hm.keySet()) {
            if (hm.get(o).equals(value)) {
                rtn.add(o);
            }
        }
        return rtn;
    }

    private static void listaMap(Map<String, String> map, Map<String, Integer> map2, File filename) {
        if (map != null) {
            try (FileWriter writer = new FileWriter(filename)) {
                for (String key : map.keySet()) {
                    String value = map.get(key);
                    Integer error = map2.get(key);
                    if (value == null) {
                        System.out.println("Warning: " +
                                key + " in listaMap.");
                        value = "Not sure";
                    }
                    writer.write(key.trim());
                    writer.write('\n');
                    writer.write(value.trim());
                    writer.write('\n');
                    if(error != null)
                        writer.write(error + "\n");
                    else
                        writer.write("0" + "\n");
                }
            } catch (IOException e) {
                System.out.println("Issue: " + filename +
                        " in listaMap");
            }
        }
    }

    private static void listaList(LinkedList<String> list2, File filename) {
        if (list2 != null) {
            try {
                FileWriter writer = new FileWriter(filename);
                for (String s : list2) {
                    writer.write(s + "\n");
                }
                writer.close();
            } catch (IOException e) {
                System.out.println("Issue: " + filename +
                        " in listaMap");
            }
        }
    }

    public static void main(String[] args) throws Exception {

        if (args.length > 0 ) {
            for (int i = 0; i < args.length; i++) {
                switch (args[i]) {
                    case "-import":
                        importFile += args[i + 1];
                        break;
                    case "-export":
                        exportFile += args[i + 1];
                        break;
                }
            }
        }
        File file = new File(importFile);
        File file2 = new File(exportFile);

        LinkedHashMap<String, String> hashMap = new LinkedHashMap<>();
        LinkedHashMap<String, Integer> hashMap2 = new LinkedHashMap<>();
        LinkedList<String> list = new LinkedList<>();
        LinkedList<Integer> list2 = new LinkedList<>();
        File file4 = new File("./capitals.txt");
        File file5 = new File("./capitalsNew.txt");
        File file3 = new File("testLog.txt");


        if (args.length == 4) {
            if ((args[0].equals("-import") & args[2].equals("-export")) |
                    (args[0].equals("-export") & args[2].equals("-import"))) {
                int N = 0;

                try (Scanner skaner = new Scanner(file)) {
                    while (skaner.hasNext()) {
                        String question = skaner.nextLine();
                        String answer = skaner.nextLine();
                        String error = skaner.nextLine();
                        hashMap.put(question, answer);
                        hashMap2.put(question, Integer.valueOf(error));
                        N++;
                    }
                } catch (Exception e) {
                    throw new Exception();
                }
                System.out.println(N + " cards have been loaded.");
                listaMap(hashMap, hashMap2, file2);
            }
        } else if (args.length == 2) {
            if (args[0].equals("-import")) {
                int N = 0;
                try (Scanner skaner = new Scanner(file)) {
                    while (skaner.hasNextLine()) {
                        String question = skaner.nextLine();
                        String answer = skaner.nextLine();
                        String error = skaner.nextLine();
                        hashMap.put(question, answer);
                        hashMap2.put(question, Integer.valueOf(error));
                        N++;
                    }
                } catch (Exception e) {
                    throw new Exception();
                }
                System.out.println(N + " cards have been loaded.");
            } else if (args[0].equals("-export")) {
                listaMap(hashMap, hashMap2, file2);

            }
        }

        for (; ; ) {
            System.out.println("Input the action (add, remove, import, export, ask, exit, log, hardest card, reset stats):");
            list.add("Input the action (add, remove, import, export, ask, exit, log, hardest card, reset stats):");
            BufferedReader scan = new BufferedReader(new InputStreamReader(System.in));
            String action = scan.readLine();
            list.add(action);

            switch (action) {
                case "add":
                    System.out.println("The card:");
                    list.add("The card:");
                    String frontCard = scan.readLine();
                    list.add(frontCard);
                    if (hashMap.containsKey(frontCard)) {
                        System.out.println("The card \"" + frontCard + "\"" + " already exists.");
                        list.add("The card \"" + frontCard + "\"" + " already exists.");
                        System.out.println();
                        break;
                    }
                    System.out.println("The definition of the card:");
                    list.add("The definition of the card:");
                    String backCard = scan.readLine();
                    list.add(backCard);
                    if (hashMap.containsValue(backCard)) {
                        System.out.println("The definition \"" + backCard + "\"" + " already exists.");
                        list.add("The definition \"" + backCard + "\"" + " already exists.");
                        System.out.println();
                        break;
                    }
                    hashMap.put(frontCard, backCard);
                    System.out.println("The pair (\"" + frontCard + "\"" + ":\"" + backCard + "\"" + ") has been added.");
                    list.add("The pair (\"" + frontCard + "\"" + ":\"" + backCard + "\"" + ") has been added.");
                    System.out.println();
                    break;

                case "remove":
                    System.out.println("The card:");
                    list.add("The card:");
                    String frontCard2 = scan.readLine();
                    list.add(frontCard2);
                    if (hashMap.containsKey(frontCard2)) {
                        hashMap.remove(frontCard2);
                        hashMap2.remove(frontCard2);
                        System.out.println("The card has been removed.");
                        list.add("The card has been removed.");
                        System.out.println();
                    } else {
                        System.out.println("Can't remove \"" + frontCard2 + "\"" + ": there is no such card.");
                        list.add("Can't remove \"" + frontCard2 + "\"" + ": there is no such card.");
                        System.out.println();
                    }
                    break;

                case "import":
                    int N = 0;
                    System.out.println("File name:");
                    list.add("File name:");
                    String capitals = scan.readLine();
                    list.add(capitals);
                    if (capitals.equals("capitals.txt")) {
                        try (Scanner skaner = new Scanner(file)) {
                            while (skaner.hasNext()) {
                                String question = skaner.nextLine();
                                String answer = skaner.nextLine();
                                String error = skaner.nextLine();
                                hashMap.put(question, answer);
                                hashMap2.put(question, Integer.valueOf(error));
                                N++;
                            }
                        } catch (Exception e) {
                            throw new Exception();
                        }
                        System.out.println(N + " cards have been loaded.");
                        list.add(N + " cards have been loaded.");
                        System.out.println();
                    } else if (capitals.equals("capitalsNew.txt")) {
                        Scanner skaner = null;
                        try {
                            skaner = new Scanner(file2);
                            while (skaner.hasNext()) {
                                String question = skaner.nextLine();
                                String answer = skaner.nextLine();
                                hashMap.put(question, answer);
                                N++;
                            }
                        } finally {
                            if (skaner != null) {
                                skaner.close();
                            }
                        }
                        System.out.println(N + " cards have been loaded.");
                        list.add(N + " cards have been loaded.");
                        System.out.println();
                    } else {
                        System.out.println("File not found.");
                        list.add("File not found.");
                        System.out.println();
                    }
                    break;

                case "export":
                    System.out.println("File name:");
                    list.add("File name:");
                    String capitalsNew = scan.readLine();
                    list.add(capitalsNew);
                    if (capitalsNew.equals("capitalsNew.txt")) {
                        listaMap(hashMap, hashMap2, file5);
                    } else if (capitalsNew.equals("capitals.txt")) {
                        listaMap(hashMap, hashMap2, file4);
                    }
                    System.out.println(hashMap.size() + " cards have been saved.");
                    list.add(hashMap.size() + " cards have been saved.");
                    System.out.println();
                    break;

                case "ask":
                    System.out.println("How many times to ask?");
                    list.add("How many times to ask?");
                    String enter = scan.readLine();
                    list.add(enter);
                    int y = Integer.parseInt(enter);
                    Collection<String> values = hashMap.values();

                    for (int j = 0; j < y;) {
                        for (String randomValue : values) {
                            int count = 0;
                            System.out.println("Print the definition of \"" + getKeyFromValue(hashMap, randomValue) + "\"" + ":");
                            list.add("Print the definition of \"" + getKeyFromValue(hashMap, randomValue) + "\"" + ":");
                            String answer = scan.readLine();
                            list.add(answer);
                            if (answer.equals(randomValue)) {
                                System.out.println("Correct answer.");
                                list.add("Correct answer.");
                            } else if (hashMap.containsValue(answer)) {
                                count++;
                                hashMap2.put((String) getKeyFromValue(hashMap, randomValue),
                                        hashMap2.getOrDefault((String) getKeyFromValue(hashMap, randomValue), (int) 0) + count);
                                System.out.println("Wrong answer. (The correct one is \"" +
                                        randomValue + "\"" + ", " +
                                        "you've just written the definition of \"" +
                                        getKeyFromValue(hashMap, answer) + "\"" + ".)");
                                list.add("Wrong answer. (The correct one is \"" +
                                        randomValue + "\"" + ", " +
                                        "you've just written the definition of \"" +
                                        getKeyFromValue(hashMap, answer) + "\"" + ".)");
                            } else {
                                count++;
                                hashMap2.put((String) getKeyFromValue(hashMap, randomValue),
                                        hashMap2.getOrDefault((String) getKeyFromValue(hashMap, randomValue), (int) 0) + count);
                                System.out.println("Wrong answer. The correct one is \"" + randomValue + "\"" + ".");
                                list.add("Wrong answer. The correct one is \"" + randomValue + "\"" + ".");
                            }
                            j++;
                            if (j == y) {
                                break;
                            }
                        }
                    }
                    break;

                case "exit":
                    System.out.println("Bye bye!");
                    list.add("Bye bye!");
                    for (String arg : args) {
                        if (arg.equals("-export")) {
                            System.out.println(hashMap.size() + " cards have been saved.");
                            listaMap(hashMap, hashMap2, file2);
                        }
                    }
                    System.exit(0);
                    break;

                case "log":
                    System.out.println("File name:");
                    list.add("File name:");
                    String log = scan.readLine();
                    list.add(log);
                    if (log.equals("testLog.txt")) {
                        listaList(list, file3);
                    }
                    System.out.println("The log has been saved.");
                    System.out.println();
                    break;

                case "hardest card":
                    Collection<Integer> values2 = hashMap2.values();
                    int count = 0;
                    for (Integer Value2 : values2) {
                        if (Value2 > 0) {
                            count++;
                            list2.add(Value2);
                        }
                    }
                    if (count == 1) {
                        System.out.println("The hardest card is \"" +
                                getKeyFromValue2(hashMap2, (Integer) list2.get(0)).get(0) + "\"" +
                                ". You have " + list2.get(0) + " errors answering it.");
                        list2.clear();
                    } else if (count > 1) {
                        System.out.println("The hardest cards are \"" +
                                getKeyFromValue2(hashMap2, (Integer) list2.get(0)).get(0) + "\"" +
                                ", \"" + getKeyFromValue2(hashMap2, (Integer) list2.get(1)).get(1) + "\"" + "." +
                                "You have " + list2.get(0) + " errors answering them.");
                        list2.clear();
                    } else {
                        System.out.println("There are no cards with errors.");
                    }
                    break;

                case "reset stats":
                    for (String key : hashMap2.keySet()) {
                        hashMap2.remove(key);
                    }
                    list2.clear();
                    System.out.println("Card statistics has been reset.");
                    break;
            }
        }
    }
}
