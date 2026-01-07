import random
def dist(a,b):
    return (a[0]-b[0])**2+(a[1]-b[1])**2

def path_cost(route):
    total=0
    for i in range(len(route)-1):
        total+=dist(locations[route[i]],locations[route[i+1]])
    return total

def path(route):
    return " -> ".join(str(x+1) for x in route)

def get_neig(route):
    neighbors=[]
    for i in range(1,len(route)-2):
        for j in range(i+1,len(route)-1):
            temp=route[:]
            temp[i],temp[j]=temp[j],temp[i]
            neighbors.append(temp)
    return neighbors

def steepest():
    route=[0]+random.sample(range(1,N),N-1)+[0]
    while True:
        neighbors=get_neig(route)
        best=route
        best_len=path_cost(route)
        for n in neighbors:
            l=path_cost(n)
            if l<best_len:
                best=n
                best_len=l
        if best==route:
            break
        route=best
    return route,best_len

def stochastic():
    route=[0]+random.sample(range(1,N),N-1)+ [0]
    max_try=100
    tries=0
    while tries<max_try:
        neighbors=get_neig(route)
        better=[]
        now_len=path_cost(route)
        for n in neighbors:
            L=path_cost(n)
            if L<now_len:
                better.append((n,now_len-L))
        if better:
            weights=[w for n,w in better]
            pick=random.choices(better,weights=weights)[0][0]
            route=pick
            tries=0
        else:
            tries+=1
    return route,path_cost(route)

def first_choice():
    route=[0]+random.sample(range(1,N),N-1)+[0]
    max_try=100
    tries=0
    while tries<max_try:
        i,j=random.sample(range(1,N),2)
        n =route[:]
        n[i],n[j]=n[j],n[i]
        if path_cost(n)<path_cost(route):
            route=n
            tries=0
        else:
            tries+=1
    return route,path_cost(route)

def random_restart(num=5):
    best_route=None
    best_dist=float('inf')
    for _ in range(num):
        route,d=steepest()
        if d<best_dist:
            best_route,best_dist=route,d
    return best_route,best_dist

print("Enter N:")
N = int(input())
locations=[]
for i in range(N):
    line=input()
    xy=line.strip().split(" ")
    locations.append((float(xy[0]),float(xy[1])))
print(locations)

print("Steepest-sscent hill climbing")
p,d=steepest()
print("Route:",path(p))
print(f"Total distance:{d}")

print("Stochastic hill climbing")
p,d=stochastic()
print("Route:",path(p))
print(f"Total distance:{d}")

print("First-choice hill climbing")
p,d=first_choice()
print("route:",path(p))
print(f"Total distance:{d}")

print("random-restart hill climbing")
p,d=random_restart(5)
print("route:",path(p))
print(f"Total distance:{d}")
