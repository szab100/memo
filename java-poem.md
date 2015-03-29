###Java Poem

```java
For the lack of a nail,
    throw new HorseshoeNailNotFoundException("no nails!");

For the lack of a horseshoe,
    EquestrianDoctor.getLocalInstance().getHorseDispatcher().shoot();

For the lack of a horse,
    RidersGuild.getRiderNotificationSubscriberList().getBroadcaster().run(
      new BroadcastMessage(StableFactory.getNullHorseInstance()));

For the lack of a rider,
    MessageDeliverySubsystem.getLogger().logDeliveryFailure(
      MessageFactory.getAbstractMessageInstance(
        new MessageMedium(MessageType.VERBAL),
        new MessageTransport(MessageTransportType.MOUNTED_RIDER),
        new MessageSessionDestination(BattleManager.getRoutingInfo(
                                        BattleLocation.NEAREST))),
      MessageFailureReasonCode.UNKNOWN_RIDER_FAILURE);

For the lack of a message,
    ((BattleNotificationSender)
      BattleResourceMediator.getMediatorInstance().getResource(
        BattleParticipant.PROXY_PARTICIPANT,
        BattleResource.BATTLE_NOTIFICATION_SENDER)).sendNotification(
          ((BattleNotificationBuilder)
            (BattleResourceMediator.getMediatorInstance().getResource(
            BattleOrganizer.getBattleParticipant(Battle.Participant.GOOD_GUYS),
            BattleResource.BATTLE_NOTIFICATION_BUILDER))).buildNotification(
              BattleOrganizer.getBattleState(BattleResult.BATTLE_LOST),
              BattleManager.getChainOfCommand().getCommandChainNotifier()));

For the lack of a battle,
    try {
        synchronized(BattleInformationRouterLock.getLockInstance()) {
          BattleInformationRouterLock.getLockInstance().wait();
        }
    } catch (InterruptedException ix) {
      if (BattleSessionManager.getBattleStatus(
           BattleResource.getLocalizedBattleResource(Locale.getDefault()),
           BattleContext.createContext(
             Kingdom.getMasterBattleCoordinatorInstance(
               new TweedleBeetlePuddlePaddleBattle()).populate(
                 RegionManager.getArmpitProvince(Armpit.LEFTMOST)))) ==
          BattleStatus.LOST) {
        if (LOGGER.isLoggable(Level.TOTALLY_SCREWED)) {
          LOGGER.logScrewage(BattleLogger.createBattleLogMessage(
            BattleStatusFormatter.format(BattleStatus.LOST_WAR,
                                         Locale.getDefault())));
        }
      }
    }

For the lack of a war,
    new ServiceExecutionJoinPoint(
      DistributedQueryAnalyzer.forwardQueryResult(
        NotificationSchemaManager.getAbstractSchemaMapper(
          new PublishSubscribeNotificationSchema()).getSchemaProxy().
            executePublishSubscribeQueryPlan(
              NotificationSchema.ALERT,
              new NotificationSchemaPriority(SchemaPriority.MAX_PRIORITY),
              new PublisherMessage(MessageFactory.getAbstractMessage(
                MessageType.WRITTEN,
                new MessageTransport(MessageTransportType.WOUNDED_SURVIVOR),
                new MessageSessionDestination(
                  DestinationManager.getNullDestinationForQueryPlan()))),
              DistributedWarMachine.getPartyRoleManager().getRegisteredParties(
                PartyRoleManager.PARTY_KING ||
                PartyRoleManager.PARTY_GENERAL ||
                PartyRoleManager.PARTY_AMBASSADOR)).getQueryResult(),
        PriorityMessageDispatcher.getPriorityDispatchInstance())).
      waitForService();

All for the lack of a horseshoe nail.
```