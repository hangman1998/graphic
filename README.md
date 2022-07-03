## each agent has the following:
AgentType type;
currentNode;
speed 
Graph map
int id
Team team
double money

* agents are in a node
* edges have prices, edges are of types: road bus train
* polices start from police station
* polices receive money as they wage
* they can move from one node to another if there is an edge between the nodes
* traversing nodes costs money
* they have money which is able to inc/dec
* there can be mulltiple agents in one node
* we have 2 channels for each team. one for polices and one for robbers.
* sending messages costs  money !!



---
```csharp
AgentType
{
    POLICE,
    THIEF
}

Team
{
    FIRST,
    SECOND
}


0: FIRST team, THIEF
1: FIRST team, POLICE
2: SECOND team, THIEF
3: SECOND team, POLICE


public enum EdgeType
{
    ROAD,
    BUS,
    TRAIN
}


roadCost = 0, busCost = 10, trainCost = 100;


public int GetPoliceStation(Team team)
{
    //return team == Team.FIRST ? 0 : 4;
    return 1;
}


private List<Agent> _agentsInNode = new();

Regex wage = new Regex("\"wage\":\"([^\"]+)\"");


  AGENT_MOVEMENT
        {
            var agentIdValue = int.Parse(GetValue(agentId, line));
            var balanceValue = GetValue(balance, line);
            var priceValue = double.Parse(GetValue(price, line), CultureInfo.InvariantCulture);
            var toNodeIdValue = int.Parse(GetValue(toNodeId, line));
            var fromNodeIdValue = int.Parse(GetValue(fromNodeId, line));

            agentsController.MoveAgent(agentIdValue, fromNodeIdValue, toNodeIdValue);
            agentsController.DecreaseBalance(agentIdValue, priceValue);
        }


    AGENT_BALANCE_CHARGED
        {
            var agentIdValue = int.Parse(GetValue(agentId, line));
            var balanceValue = double.Parse(GetValue(balance, line), CultureInfo.InvariantCulture);
            var wageValue = double.Parse(GetValue(wage, line), CultureInfo.InvariantCulture);

            agentsController.BalanceCharge(agentIdValue, balanceValue, wageValue);
        }
    AGENT_SEND_MESSAGE
        {
            var agentIdValue = int.Parse(GetValue(agentId, line));
            var priceValue = double.Parse(GetValue(price, line), CultureInfo.InvariantCulture);
            var teamValue = GetValue(team, line);
            var textValue = GetValue(text, line);
            var typeValue = GetValue(type, line);

            chatManager.UpdateChat(teamValue, typeValue, agentIdValue.ToString(), textValue);
            agentsController.DecreaseBalance(agentIdValue, priceValue);
        }
    POLICES_CAUGHT_THIEVES
        {
            var thiefIdValue = GetValue(thiefId, line);
            var nodeIdValue = GetValue(nodeId, line);
            //call function
        }
```