# find the maximum number of meeting can be possible in one meeting room

```java
  public static int maxMeetings(int start[], int end[], int n)
    {
        List<Meeting> meet = new ArrayList<>();
        for(int i=0;i<n;i++){
            meet.add(new Meeting(start[i], end[i]));
        }
        Collections.sort(meet, new Comparator<Meeting>(){
            @Override
            public int compare(Meeting first, Meeting second) {
                if(first.end != second.end){
                    return first.end < second.end ? - 1 : 1;
                }
                return first.start < second.start ? -1 : 1;
            }
            
        });
        
        int count = 1;
        int busyTill = meet.get(0).end;
        for(int i=1;i<meet.size();i++){
            if(meet.get(i).start > busyTill){
                count++;
                busyTill = meet.get(i).end;
            }
        }
    return count;
    }
```