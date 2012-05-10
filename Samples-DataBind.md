Fastjson full support databind, it's simple to use.

# Encode

    Group group = new Group();
    group.setId(0L);
    group.setName("admin");

    User guestUser = new User();
    guestUser.setId(2L);
    guestUser.setName("guest");

    User rootUser = new User();
    rootUser.setId(3L);
    rootUser.setName("root");

    group.getUsers().add(guestUser);
    group.getUsers().add(rootUser);

    String jsonString = JSON.toJSONString(group);

    System.out.println(jsonString);

# Group.java
	public class Group {
	
	    private Long       id;
	    private String     name;
	    private List<User> users = new ArrayList<User>();
	
	    public Long getId() {
	        return id;
	    }
	
	    public void setId(Long id) {
	        this.id = id;
	    }
	
	    public String getName() {
	        return name;
	    }
	
	    public void setName(String name) {
	        this.name = name;
	    }
	
	    public List<User> getUsers() {
	        return users;
	    }
	
	    public void setUsers(List<User> users) {
	        this.users = users;
	    }
	}

# User.java
	public class User {
	
	    private Long   id;
	    private String name;
	
	    public Long getId() {
	        return id;
	    }
	
	    public void setId(Long id) {
	        this.id = id;
	    }
	
	    public String getName() {
	        return name;
	    }
	
	    public void setName(String name) {
	        this.name = name;
	    }
	}